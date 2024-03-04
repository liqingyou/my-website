---
title: MongoDB Shell
description: MongoDB Shell
---

### 更新
```
db.collection.update(<query>,<update>,
   {
     <options>
   }
)
```
#### example:
```
db.users.update(
   { status: "active" },
   { $set: { status: "inactive" } },
   { upsert: false, multi: true }
)
```