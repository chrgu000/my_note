- #### 删除表中的数据的方法有`delete`,`truncate`, 其中TRUNCATE TABLE用于删除表中的所有行，而不记录单个行删除操作。`TRUNCATE TABLE` 与没有 `WHERE` 子句的 DELETE 语句类似；但是，`TRUNCATE TABLE` 速度更快，使用的系统资源和事务日志资源更少

	-  `DELETE` 语句每次删除一行，并在事务日志中为所删除的每行记录一项。`TRUNCATE TABLE` 通过释放存储表数据所用的数据页来删除数据，并且只在事务日志中记录页的释放
-  `TRUNCATE TABLE` 删除表中的所有行，但表结构及其列、约束、索引等保持不变。新行标识所用的计数值重置为该列的种子。如果想保留标识计数值，请改用 `DELETE`。如果要删除表定义及其数据，请使用 `DROP TABLE` 语句
	-  对于由 `FOREIGN KEY` 约束引用的表，不能使用 `TRUNCATE TABLE`，而应使用不带 `WHERE` 子句的 `DELETE` 语句。由于 `TRUNCATE TABLE` 不记录在日志中，所以它不能激活触发器
-  `TRUNCATE TABLE` 不能用于参与了索引视图的表
	-  对用`TRUNCATE TABLE`删除数据的表上增加数据时，要使用`UPDATE STATISTICS`来维护索引信息
-  如果有`ROLLBACK`语句，`DELETE`操作将被撤销，但`TRUNCATE`不会撤销
	
- #### 不能对以下表使用 `TRUNCATE` `TABLE`

	-  由 `FOREIGN` `KEY` 约束引用的表。（您可以截断具有引用自身的外键的表。）

	-  参与索引视图的表。

	-  通过使用事务复制或合并复制发布的表。

	-  对于具有以上一个或多个特征的表，请使用 `DELETE` 语句。

	-  `TRUNCATE` `TABLE` 不能激活触发器，因为该操作不记录各个行删除。

- #### `TRUNCATE`、`Drop`、`Delete`区别

	-  `drop`和delete只是删除表的数据(定义),drop语句将删除表的结构、被依赖的约束(`constrain`)、触发器 (`trigger`)、索引(`index`);依赖于该表的存储过程/函数将保留,但是变为`invalid`状态。

	-  `delete`语句是DML语言,这个操作会放在rollback segement中,事物提交后才生效;如果有相应的触发器(trigger),执行的时候将被触发。`truncate`、`drop`是DDL语言,操作后即 生效,原数据不会放到rollback中,不能回滚,操作不会触RU发trigger。

	-  `delete`语句不影响表所占用的extent、高水线(high watermark)保持原位置不动。`drop`语句将表所占用的空间全部释放。`truncate`语句缺省情况下将空间释放到minextents的 extent,除非使用reuse storage。`truncate`会将高水线复位(回到最初)。

	-  效率方面:`drop` > `truncate` > `delete`

	-  安全性:小心使用`drop`与`truncate`,尤其是在 没有备份的时候,想删除部分数据可使用`delete`需要带上where子句,回滚段要足够大,想删除表可以用drop,想保留表只是想删除表的所有数据、 如果跟事物无关可以使用`truncate`,如果和事物有关、又或者想触发 trigger,还是用`delete`,如果是整理表内部的碎片，可以用`truncate`跟上reuse stroage，再重新导入、插入数据。

	-  `delete`是DML语句,不会自动提交。`drop`/`truncate`都是DDL语句,执行后会自动提交。

	-  `drop`一般用于删除整体性数据 如表，模式，索引，视图，完整性限制等；delete用于删除局部性数据 如表中的某一元组

	-  `DROP`把表结构都删了；`DELETE`只是把数据清掉

	-  当你不再需要该表时， 用 `drop`；当你仍要保留该表，但要删除所有记录时， 用 `truncate`；当你要删除部分记录时（always with a WHERE clause), 用 delete.