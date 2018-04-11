- 添加数据

dbContext.entity.Add(entity);

- 删除数据

dbContext.entity.Remove(entity);

- 修改数据

修改数据相对比较麻烦，我们需要先获取entity，然后将新实体（newEntity）的字段值赋给我们的旧实体（entity）,最后在调用SaveChanges()进行提交
```
var newEntity = dbContext.entity.Find(id);
entity.field1_value = newEntity.field1_value;
entity.field2_value = newEntity.field2_value;
entity.field3_value = newEntity.field3_value;
...
entity.fieldN_value = newEntity.fieldN_value;
dbContext.SaveChanges();
```

- 查询数据

查询数据通常就比较简单了,通过dbContext.entity.ToList()我们就可以获取列表所有数据，而通常我们遇到的场景

1. 通过id（或某个字段）获取实体 
2. 通过分页获取实体列表

```
//通过字段获取实体
var entity = dbContext.entity.Find(id);

//通过分页获取实体列表
var list = dbContext.entity.OrderBy(e=>e.id)
	.Skip( (page-1)*page_size )
	.Take( page_size ).ToList();
```