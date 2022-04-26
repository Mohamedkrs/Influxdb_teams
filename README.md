# teams.endpoint
Basic Example:
```
url= "https://..."
endpoint = endpoint(url: url)
mentions = addMention(name : "team user name",id:"team user ID")
button = addButton(type: "Action.OpenUrl", title: "Go To Google.com", url:"google.com" )
crit_statuses =from(bucket: "bucket")
  |> range(start: -15s)
  |> filter(fn: (r) => r["_measurement"] == "win_cpu")
  |> endpoint(mapFn: (r) => ({
      title: "Memory Usage",
      text: "<at>team user name</at>: ${r.host}: Process uses ${r._value} GB",
      summary: "Alert",
      mention: mentions,
      button : button + button
    }),
  )()
```
