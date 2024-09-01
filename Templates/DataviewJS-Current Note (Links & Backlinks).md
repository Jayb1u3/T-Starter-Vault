```dataviewjs
dv.list(dv.current().file.inlinks.sort((a, b) => b.mtime - a.mtime));
```