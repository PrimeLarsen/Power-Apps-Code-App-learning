# Module 1 — Environment & connection

## 1. Enable Code Apps on the environment (admin)

Code Apps must be turned on per environment. A Power Platform admin or environment admin:

1. Open the [Power Platform admin center](https://admin.powerplatform.microsoft.com)
2. **Manage** → **Environments** → select the workshop environment
3. **Settings** → expand **Product** → **Features**
4. Find **Power Apps code apps** → turn on **Enable code apps**
5. **Save**

> 💡 Larger organizations: use environment groups + rules to enable this on multiple environments at once.

**Use a dedicated dev/test environment for the workshop — never production.**

## 2. Sign in with the PAC CLI

In your terminal:

+BQ+BQ+BQ+bash
pac auth create
+BQ+BQ+BQ+

Sign in with the account that has access to the environment. Working across multiple tenants? Use +BQ+pac auth create --name <profile>+BQ+ and switch with +BQ+pac auth select --name <profile>+BQ+.

## 3. Select the environment

+BQ+BQ+BQ+bash
# list all your environments
pac env list

# select the workshop environment (id, url, or unique name)
pac env select --environment <environment-id-or-url>

# verify
pac auth list
+BQ+BQ+BQ+

✅ **Checkpoint:** +BQ+pac auth list+BQ+ shows the correct environment.
