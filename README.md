# React Data Grid — Built from Scratch

A fully featured data grid component built with React hooks. No libraries used for the grid logic.

## Features
- Sorting (click any column header)
- Live search / filtering
- Pagination
- Column show/hide toggles
- Inline cell editing (with API call on commit)
- Loading skeleton
- Stats summary bar
- Status badges

## Folder Structure

```
src/
  components/DataGrid/
    index.jsx           ← root, owns all state, calls API
    Toolbar.jsx         ← search + column toggles
    TableHeader.jsx     ← sortable column headings
    TableBody.jsx       ← renders rows + loading skeleton
    TableRow.jsx        ← one row, handles inline editing
    Pagination.jsx      ← page navigation
    DataGrid.css        ← all styles
    hooks/
      useSort.js        ← sort state + handler
      useFilter.js      ← search state + handler
      usePagination.js  ← page state + navigation
      useColumnToggle.js← hidden columns Set
      useInlineEdit.js  ← editing cell + API commit
  api/
    employeeApi.js      ← API layer (swap to real fetch here)
    index.js            ← single export point
  services/
    mockServer.js       ← fake backend (filter/sort/paginate)
    delay.js            ← simulates network latency
  constants/
    columns.js          ← column config (drives the whole grid)
    mockData.js         ← 30 rows of employee data
  App.jsx
  main.jsx
```

## How the API works

`mockServer.js` is your fake backend. It:
- Filters by search query
- Sorts by any column
- Paginates results
- Has CRUD operations (GET, PUT, DELETE, POST)

`employeeApi.js` is the API layer. It wraps mockServer calls.
When you get a real backend, replace only `employeeApi.js` — nothing else changes.

## Run it

```bash
npm install
npm run dev
```

## How to swap to a real API

In `src/api/employeeApi.js`, replace each mockServer call with a real fetch:

```js
// Before (mock):
const result = await getEmployees(params);

// After (real API):
const res    = await fetch(`/api/employees?search=${params.search}&page=${params.page}`);
const result = await res.json();
```
