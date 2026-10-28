# Exercise 5 — Build an app with a connector (60 min)

**Goal:** Turn your app into a real data app. **Pick one path** — A or B — and build the same thing. Pairs are encouraged to split: one takes Dataverse, one takes SharePoint, and you compare notes at the end.

## Setup (workshop lead provides)

- **Path A (Dataverse):** a Dataverse table in the workshop environment, e.g. `cr123_workshoptasks` with columns: Title (text), Done (Yes/No), Due (date)
- **Path B (SharePoint):** a SharePoint site with a list, e.g. "Workshop Tasks" with columns: Title, Done (Yes/No), Due (date)

## Part A: Add the data source (10 min)

**Dataverse path:**

`BQ`bash
pa app add data-source --connector dataverse --table <table-logical-name>
`BQ`

**SharePoint path:**

`BQ`bash
pa connection create                  # save the Connection ID
pa app add data-source                # interactive mode — pick your connection, site, and list
`BQ`

Inspect what was generated in `src/generated/services/` — open the service file and find the typed methods.

## Part B: Build the CRUD UI (35 min)

Using the generated service, build:

1. **List:** show all tasks (use `getAll` with `top: 50`)
2. **Create:** input + button that creates a task
3. **Update:** toggle the "Done" column on a task (update **only the changed field**)
4. **Delete:** remove a task from the list
5. **Filter/sort bonus:** add a search box using the `filter` option — remember it's **delegated**, so don't filter client-side

Test locally with `npm run dev`. Data operations work in Local Play too.

## Part C: Publish & share (15 min)

`BQ`bash
npm run build
pac code push
`BQ`

**Definition of done:** a colleague can open your app, add a task, tick it off, and the change is visible in Dataverse or the SharePoint list.

## Compare notes in plenum

| Question | Dataverse path | SharePoint path |
|---|---|---|
| Connection setup | none (native) | connection ID + site + list |
| Where does data live? | Dataverse of the environment | SharePoint site |
| Generated code | same pattern | same pattern |
| Server-side filter/sort? | delegated | delegated |
| When would you pick this? | enterprise app, relational data, security roles | quick team tool, files/collaboration, existing site |

---

## Bonus (for the fast ones)

- Add `pa app refresh data-source` to your notes — then have the workshop lead add a column to the table/list, refresh, and use the new column in code
- Try adding SharePoint **actions** (`--as action`) alongside the list
- Look up what a **connection reference** is and sketch how it would change your deploy pipeline (module 8, section 6)
