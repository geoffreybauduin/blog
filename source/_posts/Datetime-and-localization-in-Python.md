---
title: Datetime and localization in Python
date: 2016-05-16 14:03:48
tags:
- python
---

Last week, I came across an issue we frequently have on our architecture, at work. We are testing our software with SQLite on our computers, but the production server isn't based on SQLite (don't worry, we have a huge pipeline with testing to ensure this is working).

A common issue we have, with SQLite, are date fields. Indeed, they are not localized in SQLite, and this is sometimes very annoying. We came up with this little workaround that I thought like sharing with you:

```python
import pytz

def localize_date(date):
    try:
        return pytz.utc.localize(date)
    except ValueError:
        # Exception raised if the date is already localized
        return date

```