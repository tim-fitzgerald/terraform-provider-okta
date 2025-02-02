---
layout: 'okta' 
page_title: 'Okta: okta_app' 
sidebar_current: 'docs-okta-datasource-app' 
description: |- 
  Get an application of any kind from Okta.
---

# okta_app

Use this data source to retrieve an application from Okta.

## Example Usage

```hcl
data "okta_app" "example" {
  label = "Example App"
}
```

## Arguments Reference

- `label` - (Optional) The label of the app to retrieve, conflicts with `label_prefix` and `id`. Label uses
  the `?q=<label>` query parameter exposed by Okta's API. It should be noted that at this time the API searches both `name`
  and `label` with a [starts with query](https://developer.okta.com/docs/reference/api/apps/#list-applications) which
  may result in multiple apps being returned for the query. The data source further inspects the lables looking for
  an exact match.

- `label_prefix` - (Optional) Label prefix of the app to retrieve, conflicts with `label` and `id`. This will tell the
  provider to do a `starts with` query as opposed to an `equals` query.

- `id` - (Optional) `id` of application to retrieve, conflicts with `label` and `label_prefix`.

- `active_only` - (Optional) tells the provider to query for only `ACTIVE` applications.

- `skip_users` - (Optional) Indicator that allows the app to skip `users` sync. Default is `false`.

- `skip_groups` - (Optional) Indicator that allows the app to skip `groups` sync. Default is `false`.

## Attributes Reference

- `id` - Application ID.

- `label` - Application label.

- `name` - Application name.

- `status` - Application status.
 
- `links` - Generic JSON containing discoverable resources related to the app.

- `users` - List of users IDs assigned to the application.
  - `DEPRECATED`: Please replace all usage of this field with the data source `okta_app_user_assignments`.

- `groups` - List of groups IDs assigned to the application.
  - `DEPRECATED`: Please replace all usage of this field with the data source `okta_app_group_assignments`.
