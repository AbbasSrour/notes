---
aliases: 
tags: ['daily']
date-created: 
date-modified: 
title: Daily Planner 2
 
gesundheit:
  schritte: 
  wasser: 
  schlafdauer: 
  schlafquali: 
---
 
%*
const {getEvents} = this.app.plugins.plugins["google-calendar"].api;
 
const file = await tp.file.title;
const events = await getEvents({ startDate: window.moment(file) });
 
var eventsString = await events.reduce((text, event) => text +=`- [ ] ${moment(event.start.dateTime).format("HH:mm")} ${event.summary} \n`, "");
eventsString = eventsString.replace(/\|/g, '-');
%
 
# Daily Planner 2
 
## Health
 
```dataviewjs
var schritte = dv.current().gesundheit.schritte;
var wasser= dv.current().gesundheit.wasser
var dauer = dv.current().gesundheit.schlafdauer;
var index = dv.current().gesundheit.schlafquali;
 
var rDauer = 0;
var goals = '';
 
if (schritte == null) {schritte='-';}
if (wasser == null) {wasser='-';}
if (dauer == null) {
    dauer = '-';
} else {
    dauer = Math.round(dauer / 60 * 10) / 10;
}
if (index == null) {index='-';}
 
goals = `*Schritte*: **${schritte}**
*Wasser:* **${wasser}** Gläser
*Schlafen:* **${dauer}** Stunden (**${index}**)`;
 
dv.paragraph(goals);
```
 
## Journal
 
## Ideas
 
## Day Planner
%`${eventsString}`%
 
## To Do
 
## Backlinks
 
```dataview
LIST
FROM [[Daily Planner 2]]
WHERE !contains(tags, "waypoint")
AND !contains(file.name, "_")
AND !contains(file.name, "+")
AND !contains(file.name, "%")
AND !contains(file.path, "Daily Notes")
```