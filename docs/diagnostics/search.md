---
title: Search in Diagnostics
description: A description of the search functionality in Diagnostics
keywords: crashes, errors, search
author: blparr
ms.author: blparr
ms.date: 10/09/2019
ms.topic: article
ms.assetid: 92ABCD39-D03A-4560-BE32-31C44DE1EAC6
ms.service: vs-appcenter
ms.custom: analytics
---

# Search in Diagnostics

In this section, you will learn about the ability to search Diagnostics data in App Center.

## How to use Search

App Center Diagnostics allows you to search for specific crashes and handled errors. In the Diagnostics overview, click on the magnifying glass to start using Search.

![App Center Diagnostics search](~/diagnostics/images/search-overview.png)

### Search types

App Center searches in the indexed fields, and can be done in two ways:

1. Use the search box to include free text. Note that this text will be searched in just the indexed fields.

  ![Free text search](~/diagnostics/images/crashes-results-freetext.png)

2. Use the query builder to specify what fields you want to search on by clicking on the filtering icon.

  ![Query builder](~/diagnostics/images/crashes-query-types.png)

3. If your Xamarin or Unity app is tracking handled errors you can specify the type of issue you want to search next to the search box.

  ![Search type selection](~/diagnostics/images/search-type-selection.png)

### Indexed fields

For crash and error reports:

- User ID
- Method
- Class
- Exception Type
- Reason
- Model
- OS Version

For crash and error groups:

- Method
- Class
- Exception Type
- Reason

## Considerations

- Only symbolicated crashes are searchable; you must upload the symbols to search for them.
- The maximum number of matching reports we display is 100.
- For now, search results show the last 30 days of data, regardless of the retention settings.
