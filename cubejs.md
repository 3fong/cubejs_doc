## cube.js基础

cube.js是一个开源分析api平台.主要用于构建内部业务智能工具和对已有应用添加面向用户的分析.

数据分析工具存在的问题:

- 性能
- sql代码管理
- 基础设施


cube.js执行流程

![cube.js执行流程](./pic/FluGFqo.png)

### 核心

核心是sql解析和查询优化.基于redis或缓存来加速查询.

缓存不一致问题

### Pre-Aggregations

预聚合是源数据的压缩版本.用于构建聚合数据和刷新的层.可以显著加速查询和增加并发.

To start building pre-aggregations, Cube.js requires write access to the pre-aggregations schema in the source database. Cube.js first builds pre-aggregations as tables in the source database and then exports them into the pre-aggregations storage.

如果Cube.js找到合适的预聚合规则，则数据库查询将成为一个多阶段过程：

- Cube.js检查是否存在预聚合的最新副本。
- Cube.js将针对预聚合的表而不是原始数据执行查询。

### schema

schema:生成和执行sql

需要支持功能:

1. 自定义驱动
2. 可视化管理
3. 生产部署




cubejs是开源接口分析平台.主要用于在已有应用中构建内部商业智能工具或支持面向用户的分析能力.

实现方式:在数据上创建语义API层,用于管理访问控制,换成和数据聚合.


数据仓库:

data warehouses. Data warehouses are a deeply integrated stack of components that facilitate analytics, with features like tightly integrated scale-out storage and compute architecture, query compiler and optimiser, meta data catalog for table definitions, data loading functions, indexing components, and application client protocols and SDKs.

无服务器数据和分析平台

我们将数据和分析平台定义为一个平台，可让您存储，管理，生命周期和分析数据，并在此基础上开发分析解决方案。以下是一个全面的无服务器数据和分析平台的关键要素：

	存储即服务。
	
	用于处理元数据和治理的目录服务。
	
	数据提取服务。
	
	数据转换服务。
	
	分析和查询服务。
	
	解析应用程序运行时，业务流程和API。

![无服务器数据和分析平台](https://1.cms.s81c.com/sites/default/files/2018-11-23/Screen-Shot-2018-09-27-at-14.23.14.png)



### 多租户

1 库级租户

	通过多数据源和dbType,COMPILE_CONTEXT来支持

同一schema不同库的租户隔离示例:

	库命名为应用_应用id_用户id:my_app_1_2.这样通过库名就可以区分具体租户信息

同库租户预聚合隔离

	CUBEJS_APP_${securityContext.userId}	
	pre_aggregations_${securityContext.userId}

dbType:多驱动多schema.某一租户的驱动和schema不同的情形

	driverFactory:驱动工厂(database)
	repositoryFactory:库工厂(schema)

2 行级租户

	SECURITY_CONTEXT:where条件显示过滤
	queryTransformer:sql执行前查询检查的安全钩子.在原始查询中添加租户过滤器,使用securityContext获取当前租户信息

问题:

COMPILE_CONTEXT可以影响编译结果,它是如何生效的?

### 缓存应用 ###

Compiler
refreshKey
cache
schema

### 预聚合 ###

预聚合是源数据的压缩版本


问题:无法命中该预聚合

	preAggregations: {
	    categoryAndDate: {
	      type: `rollup`,
	      measureReferences: [count],
	      dimensionReferences: [address,tenant],
	      timeDimensionReference: [ts],
	      granularity: `day`
	    },
	  },






































