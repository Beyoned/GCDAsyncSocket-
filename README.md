# GCDAsyncSocket-
利用GCDAsyncSocket第三方框架编写的简单局域网聊天室（内含客户端代码和服务端代码）,主要目的是学习Socket编程

#Core Data-

CoreData和我们的Sqlite是不冲突的，都是数据持久化用的，开发商不一样。Sqlite是C级的，是属于开源的，而我们的CoreData是我们苹果公司开发的，我们的Sqlite支持的是.sqlite类型的文件。而我们的CoreData支持的文件类型分为三大类
第一是Sqlite类文件，第二是binary文件（二进制），第三个是XML类文件

注：CoreData是一个框架，

- NSManagedObjectContext 管理对象，上下文，持久性存储模型对象
- NSManagedObjectModel 被管理的数据模型，数据结构
- NSPersistentStoreCoordinator 连接数据库的
- NSManagedObject 被管理的数据记录
- NSFetchRequest 数据请求
- NSEntityDescription 表格实体结构

一、 NSPersistentStoreCoordinator(Persisetnt的意思是持久、Store的意思是存储、Coordinator的意思就是协调者，助理）
NSPersistentStoreCoordinator的意思就是数据持久存储助理，这是一个核心，所有的东西都是由它来控制，它就相当于一个桥梁纽带,在它下面有一个PersistentStore，这个类主要是关联我们的文件的

二、另外一个和它密切合作的是ManagedObjectModel,被管理对象的模型。
说简单一点它就相当于一个集合，是一个容器，他里面放得都是实体（Entity）通俗一点就是“表”
所有的表都被他管理，它就相当于一个数据库一样。在我们的iOS里被称之为实体描述,这些都是底层的东西

三、我们主要接触的叫做ManagedObjectContext（被管理者上下文),你可以理解它为一个临时数据库。

他们之间的关系就是NSPersistentStoreCoordinator根据需求向file文件获取内容后拿去给ManagedObjectContext
我们的这个NSPersistentStoreCoordinator助理不仅可以从本地读取文件，也可以在网络上读取。并且呢，我们还可以从本地读取文件后存到网上,我们平时读数据库就是获取我们的数据库路径后再读文件。

但是你使用CoreData的话就不一样的，我们使用的是一个URL，它可以标示一个网络路径也可以标示一个本地路径，这就是它的强大之处。 用到一个新的类NSFetchRequest(Fetch的意思是获取读取) 获取一个请求，读取一个请求

它会告诉我们他要获取哪个表，他不跟底层的类联系，他只和ManagedObjectContext联系,是对ManagedObjectContext的一个操作。

ManagedObjectContext可以有一个，也可以有多个，它可以对应多个文件，也可以对应半个文件
NSPersistentStoreCoordinator可以从多个文件中整理出来数据拿给ManagedObjectContext
NSFetchRequest是从我们的ManagedObjectContext中读取数据的，并不是向底层的文件读取

不管你使用ManagedObjectContext如何修改，底层的文件是不受影响的，但是我们如果想要更改
底层的文件的话，可以让我们的ManagedObjectContext调用一个save的方法进行保存一下即可
ManagedObjectContext也就是数据集的一个映射，他不是真实数据，但是可以影响真实数据
 
