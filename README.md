# Wagtail Multilingual

The goal of this project is to create a Wagtail add-on that makes it trivial to support multilingual content in a [Wagtail](//github.com/wagtail/wagtail) site. There are a few other solutions for this, perhaps most notably the [wagtailtrans](//github.com/wagtail/wagtailtrans) and the [wagtail-modeltranslation](//github.com/infoportugal/wagtail-modeltranslation) packages. However, for our use case there are a few constraints that make neither option tenable.

## Rationale

At [AL Downtown](//aldowntown.com) we needed a translation package for Wagtail that provide a neat and intuitive translation interface for site editors, while being trivial to **add and remove** to an **existing website**. Hence, using something like wagtailtrans is not an option for our use case as it requires you to inherit from their base model. wagtail-modeltranslation is more promising in this regard as it is using a registration approach to add model fields for each translated field and language. However, this can quickly lead to a large number of fields as the number of supported languages increases, and adding any new field or language will require a new set of database migrations. While not strictly a hinderance to our goal of easily adding and removing translations to existing page models, it arguably becomes messy and may result in unexpected consequences for developers working on other apps within the same Wagtail site that now requires new migration for every model change.

## Goals

- Make page content translatable for existing Page models
  - Do not require any changes to model inheritance
- Perform minimal database migrations when adding/removing fields and/or languages
- Make it possible to edit different translations side-by-side, or at least inline
- Apply translations in views without any changes to existing templates

