---
title: Introduction
slug: intro
description: Get acquainted with Laramie
---

## Intro

Laramie is a magical composer package for [Laravel](https://laravel.com/) that grants your application amazing CMS abilities. Installation is totally non-destructive, so you can install it and not worry about it wrecking existing work. Drop it in and leverage it for your whole application or just parts of it.

Like other magic, it comes at a cost. You should probably know what that is up front:
- First, it's a package _for_ Laravel, so Laravel is a requirement. Easy.
- Laramie's juju requires running postgres 9.4 or greater (for now). So if you're dropping it into an existing app, it won't work if you're on MySQL.
- Not strictly required, but you'll likely want to access Laramie-controlled data via a Laramie service rather than Eloquent (again, Laramie is not an all-or-none proposition. Use Laramie just where it makes sense).

If you can live with those things, Laramie might just be the CMS for you. Why?

- Non-destructive installation
- Security. It leverages Laravel's excellent [authentication framework](https://laravel.com/docs/authentication) and adds fine-grained permissions and two-factor authentication on top.
- Version **all** content: view history and roll back when needed
- Exposes a robust Contentful-like API
- Custom workflows via event hooks
- Advanced filtering and sorting and the ability to save reports, export to CSV, etc
- Fine grain permissions and customizable roles
- Simple data modeling (JSON)
- Easy relationships between models (single, many)
- Aggregate fields (allows one to group fields together)
- Repeatable aggregates
- Validation hooks for all field types (directly leverage [Laravel's validation](https://laravel.com/docs/validation), or add complex custom validation via event listeners).
- Tons of field types including:
  - Most HTML-5 fields (color, date, datetime-local, email, month, number, tel, text, time, url, week, textarea, etc)
  - Computed (strictly for reporting)
  - WYSIWYG fields
  - Markdown with preview
  - Aggregate (container for other fields of any type)
  - etc
- Lots more