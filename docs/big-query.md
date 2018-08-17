# Big query

?> To query all days just use asterisk `*` symbol in a date eg: `2018*`, `201808*`

## UNNEST

First check schema, to see which fields are array[], for those we need to unnest them with a function like this:

```SQL
SELECT
  COUNT(*) as SuccessCredential
FROM
  `smartkarma-prod.analytics_XXXXXX.events_201808*`,
  UNNEST (event_params) AS event_param
WHERE
  event_name = 'user_logged_in'
  AND event_param.value.string_value = 'Credentials'
```

## Useful queries

### Get User ID from user_pseudo_id

```SQL
SELECT
  DISTINCT user_id
FROM
  `smartkarma-prod.analytics_XXXXXX.events_201808*`
WHERE
  user_pseudo_id = 'XXXXXXXXXXXXXXXXXXXX'
  AND user_id IS NOT NULL
```
