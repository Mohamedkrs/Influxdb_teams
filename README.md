# teams.endpoint
This Repository in based on https://github.com/influxdata/flux/tree/v0.113.1/stdlib/contrib/sranka teams code and adds extra features like mentions and buttons.

Basic Example:
Copy [teams](https://github.com/Mohamedkrs/Influxdb_teams/blob/main/teams.flux) into a task in influxdb and add the next code at the end.
This Example adds a mention for *Tom Cruise* with its respective teams ID ( use [Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer) to get the correct IDs). It's possible to add multiple mentions as follow:
> mentions = addMention(name : "James Bond",id:"007") + addMention(name : "Tom Cruise",id:"123456")

Adding Button / Buttons
> button = addButton(type: "Action.OpenUrl", title: "Go To Google.com", url:"google.com" )

> button2 = addButton(type: "Action.OpenUrl", title: "Go To Mohameds GITHUB", url:"https://github.com/Mohamedkrs" )
```
url= "https://..."
endpoint1 = endpoint(url: url)
mentions = addMention(name : "James Bond",id:"007")
button = addButton(type: "Action.OpenUrl", title: "Go To Google.com", url:"google.com" )
button2 = addButton(type: "Action.OpenUrl", title: "Go To Mohameds GITHUB", url:"https://github.com/Mohamedkrs" )
crit_statuses =from(bucket: "bucket")
  |> range(start: -15s)
  |> filter(fn: (r) => r["_measurement"] == "win_cpu")
  |> endpoint1(mapFn: (r) => ({
      title: "Memory Usage",
      text: "<at>team user name</at>: ${r.host}: Process uses ${r._value} GB",
      summary: "Alert",
      mention: mentions,
      button : button + button1
    }),
  )()
```
