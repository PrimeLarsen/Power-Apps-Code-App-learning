# Module 8 — Connectors: Dataverse or SharePoint

This module makes the app *useful*: participants connect a real data source and build CRUD against it. Everyone follows the same pattern, but each participant (or pair) **picks their own data source**:

- **Path A — Dataverse** (native, no connection ID needed)
- **Path B — SharePoint list** (classic connector with connection + site + list)

## 1. How connector access works in a Code App

You don't hand-write REST calls. The Power Apps CLI **generates a typed TypeScript model and service** for each data source into +BQ+src/generated/+BQ+. You import the service and call its methods — with IntelliSense, types, and paging/delegation handled for you.

> 🧠 Mindset for the team: +BQ+pa app add data-source+BQ+ is your "Add data source" button from Studio — except the output is reviewable, versioned TypeScript.

> ⚠️ **Note:** the data-source commands use the **npm-based +BQ+pa+BQ+ CLI** from the Power Apps client library for code apps (v1.0.4+), not +BQ+pac code+BQ+. Install/use it from your project root — it will eventually replace the +BQ+pac code+BQ+ commands. Publishing still goes through +BQ+npm run build+BQ+ + +BQ+pac code push+BQ+ (or +BQ+pa app push+BQ+ in newer versions).

## 2. Path A — Dataverse (native table)

**Prerequisite:** a Dataverse table in the workshop environment (e.g. a custom "Workshop Tasks" table, or a built-in table like Accounts).

From your project root:

+BQ+BQ+BQ+bash
pa app add data-source --connector dataverse --table <table-logical-name>
+BQ+BQ+BQ+

No connection ID or dataset needed — the app talks to the Dataverse of the environment it's initialized against. This generates:

- +BQ+src/generated/models/<Table>Model.ts+BQ+ — the typed data model
- +BQ+src/generated/services/<Table>Service.ts+BQ+ — typed CRUD methods

### Generated CRUD methods

+BQ+BQ+BQ+ts
import { AccountsService } from "./generated/services/AccountsService";
import type { Accounts } from "./generated/models/AccountsModel";

// CREATE
await AccountsService.create({ name: "New Account" } as Omit<Accounts, "accountid">);

// READ one
const one = await AccountsService.get(accountId);

// READ many (with delegation!)
const result = await AccountsService.getAll({
  select: ["name", "accountnumber"],
  filter: "address1_country eq 'USA'",
  orderBy: ["name asc"],
  top: 50,
});

// UPDATE (only changed fields!)
await AccountsService.update(accountId, { name: "Updated Name" });

// DELETE
await AccountsService.delete(accountId);
+BQ+BQ+BQ+

The +BQ+getAll+BQ+ options (+BQ+filter+BQ+, +BQ+select+BQ+, +BQ+orderBy+BQ+, +BQ+top+BQ+, +BQ+maxPageSize+BQ+, +BQ+skipToken+BQ+) are **delegated to the server** — like +BQ+Filter+BQ+/+BQ+Sort+BQ+ in Power Fx, not client-side filtering.

**Supported:** CRUD, option set labels, table metadata, single-valued lookups, image/file upload & download (preview), paging.
**Not yet supported:** polymorphic lookups, FetchXML, alternate keys, metadata CRUD.

## 3. Path B — SharePoint list

**Prerequisite:** a SharePoint site with a list (e.g. "Travel Request" or "Workshop Tasks").

### Step 1: Create a connection (once)

+BQ+BQ+BQ+bash
# create and save the returned Connection ID
pa connection create

# or list existing connections
pa connection list
+BQ+BQ+BQ+

### Step 2: Add the list as a data source

For SharePoint, +BQ+--table+BQ+ is the **list name** (URL-encoded if it has spaces) and +BQ+--dataset+BQ+ is the **site URL**:

+BQ+BQ+BQ+bash
pa app add data-source \
  --connector "shared_sharepointonline" \
  --connection-id <your-connection-id> \
  --table "Travel%20Request" \
  --dataset "https://contoso.sharepoint.com/sites/WorkshopSite"
+BQ+BQ+BQ+

Not sure about names? Discover them first:

+BQ+BQ+BQ+bash
pa connection list-datasets --connector "shared_sharepointonline" --connection-id <id>
pa connection list-tables  --connector "shared_sharepointonline" --connection-id <id> --dataset <site-url>
+BQ+BQ+BQ+

Or just run +BQ+pa app add data-source+BQ+ with no parameters in an interactive terminal — the CLI lists connections, datasets, and lets you pick tables from a searchable list. **Recommended for the workshop.**

### Step 3 (optional): SharePoint actions

SharePoint also supports **actions** (not just list CRUD), e.g. "Create file", "Get attachments". Add them alongside the table:

+BQ+BQ+BQ+bash
pa app add data-source \
  --connector "shared_sharepointonline" \
  --connection-id <id> \
  --as action
+BQ+BQ+BQ+

## 4. Build the same UI on either path

Because both paths generate a typed service, the React code is nearly identical. Example — a task list that works with either:

+BQ+BQ+BQ+tsx
import { useEffect, useState } from "react";
import { WorkshopTasksService } from "./generated/services/WorkshopTasksService";

function TaskList() {
  const [tasks, setTasks] = useState<any[]>([]);
  const [newTitle, setNewTitle] = useState("");

  useEffect(() => {
    WorkshopTasksService.getAll({ top: 50 })
      .then((r) => setTasks(r.data ?? []))
      .catch(console.error);
  }, []);

  const addTask = async () => {
    if (!newTitle) return;
    await WorkshopTasksService.create({ title: newTitle } as any);
    setNewTitle("");
    const r = await WorkshopTasksService.getAll({ top: 50 });
    setTasks(r.data ?? []);
  };

  return (
    <div>
      <input value={newTitle} onChange={(e) => setNewTitle(e.target.value)} />
      <button onClick={addTask}>Add</button>
      <ul>
        {tasks.map((t: any) => (
          <li key={t.id}>{t.title}</li>
        ))}
      </ul>
    </div>
  );
}

export default TaskList;
+BQ+BQ+BQ+

## 5. Housekeeping commands

+BQ+BQ+BQ+bash
pa app refresh data-source --name <data-source-name>   # regenerate after schema changes
pa app remove data-source --connector <connector-id> --name <name>
+BQ+BQ+BQ+

When someone adds a column to the SharePoint list or Dataverse table, refresh regenerates the typed model — the code equivalent of refreshing a data source in Studio.

## 6. ALM tie-in: connection references

Binding an app directly to a developer's personal connection breaks when moving dev → test → prod. The proper ALM pattern is a **connection reference**: a solution component that *points to* a connection, so each environment can have its own. Add data sources via connection references when you plan real environment promotion — this is the "solution-aware" piece of Code App lifecycle. (Workshop tip: mention it here, practice it after the workshop.)

## 7. Known limitations

- **Excel Online (Business/OneDrive) connectors are not supported** — migrate spreadsheet-as-database apps to SharePoint lists, SQL, or Dataverse first
- SharePoint connection: +BQ+--table+BQ+ = list name, +BQ+--dataset+BQ+ = site URL; names are case-sensitive
- Dataverse native: one table per +BQ+add data-source+BQ+ command

✅ **Checkpoint:** your app shows live data from Dataverse or SharePoint, and you can create a record from the UI.
