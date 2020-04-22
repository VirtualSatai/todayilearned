I tried to look an hour into the past with a query like:
```
some_date_time >= NOW() - INTERVAL 1 HOUR;
```

But I didn't get any results as I expected...

This was because `some_date_time` is of MySQL type: "datetime" and "NOW()" returns a "timestamp".
They differ since "timestamp" includes a timezone in its data, and is therefore timezone aware. "datetime" is not, and is stored in UTC for this application.

Two ways of resolving this is:
1. (bad) set timezone for the query: `set time_zone = '+00:00';`
2. (good) use `UTC_TIMESTAMP()` instead of `NOW()`
