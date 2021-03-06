---
title: "定义一个好的API"
date: 2021-12-27T15:25:39+08:00
draft: false
---

大家好，今天我们聊一下什么是API，以及如何设计一个好的API。

### 什么是API？
举个现实场景的例子，我们去餐厅吃饭，通过菜单了解到餐厅提供的美食清单，指定选择菜单上的菜品，得到我们想要的餐食。虽然我们并不了解餐食是如何做出来的，仍然可以通过这一方式获得想要的结果。这个过程，换成程序语言，就是一个调用API，获得结果的过程。
在一个编程的角度来说，API，Application Programming Interface，是预先定义好的一个应用程序接口。可以根据约定，提供外部系统或人员需要的应用程序内部的数据，而又不需要了解程序内部的实现过程或细节。
举个例子，梦想书城的项目开发中有一个动作，根据作者姓名得到作者信息。那么这个动作应该提供一个API，getAuthors，提供返回的作者们的名称，包括可能找不到作者的场景，提供一个查找不到的响应标识。
常见的API有很多，Web标准协议Restful API，Windows的动态链接库，Linux的POSIX等。一个API通常由方法名，参数和返回值组成，这和编程开发中的函数很像，明显的区别是是否屏蔽内部实现。
​
### 什么是好的API？
首先我们要明确，API是为了让外部系统调用的。那么最重要的一点，就是可以清楚的告诉外部系统，能得到什么，不能得到什么。判断一个API描述是否清楚，可以采用采用一个小技巧，遮挡住参数和返回值，能否根据方法名称猜到返回值和参数内容。
- 方法名称中要明确返回值的边界。根据刚才的梦想书城的例子getAuthors，这个API的返回结果应该有且只有一种，作者信息，仅限于作者这个模型特征的信息数据。API的数据提供方也限制在作者这个模型领域内。有一种情况，实际开发中经常会出现，调用方想要在返回结果中增加作者所在的作家协会，假如API中增加了类似的信息，那这个就不是一个合适的API定义。合适的办法是开发另外的API接口，并明确的指出返回值范围包括所属作家协会，例如getAuthorsWithOrgs。我们需要明确地返回值边界，确保getAuthors的所有使用方没有歧义。
- 方法参数要跟方法主体匹配。还是getAuthors的例子，根据这个名称，我们判断这个方法可以设置的参数大概是，作者姓名，作者年龄，性别等等，例如getAuthors（name），很多场合也可以用author.get（name）的方法，这两个含义相同，参数要限制在作者这个模型主体之内。如果有个场景是根据书名返回作者名称，那么强烈建议修改方法名称为getAuthorsByBookname，这种情况下，外部系统和开发者都很容易判定参数应该只有Bookname一种。
- 避免增加附加参数。很多“祖传”代码中常见的问题，例如getAuthors方法中，增加一个调用方的参数，并且通常能看到实现中有一段hardcode，写着如果是某个调用方，有些逻辑是特别的。这种特别的附加参数，对于方法描述是毫无意义的，但是对于外部系统调用方来说有很困惑。另一种，根据不同的附加参数，会执行不同的逻辑。假设现在有个方法setAuthor（author，org），要添加一个作者，如果作者有作家协会，同时更新所属协会。这种情况下，还是强烈建议修改名称，在方法描述中，体现出这个附加参数的含义。

### 清晰的定义一个API，对系统内部也会有很多好处。
- 降低IO开销。很多时候，一个API调用会对多个微服务模块进行调用，数据组装。这些IO调用的成本非常的昂贵。明确的API定义，能让外部系统调用方选择最准确的方法，避免无效的时间浪费。特别是现在互联网行业下，动辄数十万次的调用，累计起来的IO消耗非常大。
- 降低API重构风险。只做一件事，明确的API边界，意味着最小力度的访问关联的微服务，降低由于其他业务变化，引起的API实现逻辑变更。系统开发中，“蝴蝶效应”是非常明显的，经常会发生A系统的功能变化，莫名引起E系统的故障，一条链路上的B，C，D系统都需要跟着排查的事情。清晰的API边界能有效减少其他业务的耦合度，降低重构风险。
- 减少未来功能扩大化的风险。你永远不知道未来会发生什么，防止未来的同事，甚至自己，在这个方法中添加超出方法边界的功能，是让外部系统调用清晰以外最重要的一个价值。尽可能的做到参数准确定义，对潜在的风险给出明确的拒绝的含义。例如，getAuthorsByBookname，getAuthorsByBookId，要比GetAuthorsByBook，要好。getMaleAuthorsWithOrgs也要比getAuthorsWithOrgs（male）好很多，可以想象的未来getAuthorsWithOrgs的参数会增加到male，age，甚至create time这种非业务含义逻辑。

### 讲了最重要的方法定义，还有一些帮助我们建立好的API设计的实践经验。
- 明确的参数校验错误信息，减少不必要的参数校验。有些校验是必须的，例如非空判定，例如更新数据时的类型判断，我们要提供明确的错误信息，告知哪个字段为空，不是让外部系统猜测。但有些并不必要，可以减少API复杂度。例如查询参数过长，如果不会引起数据库异常，这个就是外部系统调用方的问题，结果只是查找不到，他们会自己发现问题。同样的，一个字符串的数值，也不需要判定是否传入一个整数，抛出奇怪的类型转换错误。尽量避免返回一个通用错误，例如，未知错误。
- 减少同时更新并查询的定义。这点在RestfulAPI上经常看到，例如想要查询作者信息，通过Get语义获得Authors，要比Post语义中返回Authors要好很多，并不仅仅是传递参数位置和大小的原因，使用Post语义容易产生更新数据的歧义。很多方法API定义中，setAuthors 或者 saveAuthors，会经常性同时返回一个结果，这样会有一定的隐患。例如我们想要增加缓存，缓存最佳实践中，建议更新的场景删除缓存，获取的场景设置缓存，这种同时返回结果，在并发的场景下，会产生脏数据，也会给使用方带来困惑。
- 明确单条和多条的查询结果使用不同的定义，多条返回结果中使用分页。例如getAuthorById，getAuthors。对于外部系统使用方，也容易判定如何使用，降低系统错误。强烈建议除非明确的返回数量含义，或者基于共识以外，要使用分页返回数据，并且给出的当前是第几页或者第几个游标。比如我们限定用户的收货地址，不超过5个，那么返回地址的API中，可以不用分页。但如果我们返回当前热销的书籍，尽量使用带分页的返回结果。也许后面的场景中，会出现最热销的100本的要求。
- API调用量很大的场合，要分片，并且有结束标识。很多时候，会需要返回大量的数据，例如调用查询最近6个月的交易情况，也许这个动作会有上百kb的数据响应包。我们需要依次把分片的数据包发送给外部接收方，并且告知最后一个数据包，进行合并。当然同样的操作，也可以在分页定义数据中完成，但这增加了网络IO的调用次数，并增加了业务的复杂度。
- 增加缓存或增加限流限速措施。这两个放在一起的原因，是他们都是为了解决系统的可用性。一个例子是系统的评论系统，大部分场景，你并不关心过去几秒钟发生的评论信息，或者用户更新了头像，其他人默认看到的是昨天的头像，并不会造成什么问题。另外一些场景，外部系统的调用方，突然地大规模的调用API，可能会引起系统故障，那么就要增加限流措施等降级措施。比如梦想书城的供应商系统突然上传全部的库存书籍，这可能是不合理的，需要做一定的限制。
- 提供版本号。这一般发生在服务方，在外部系统调用方不可控的场景下。例如移动终端APP使用的后端服务，或者供应商使用的数据传输接口。这种一经发布，不可修改的业务场景，使用版本管理API定义是非常有效的API设计。

一个好的API定义，就是一种对功能范围的明确约定。对外部系统来说，约定的范围能避免业务分期；对内部服务来说，明确地范围能有效的降低未来的功能变更的风险。

如果你对上述的内容有任何的想法和建议，欢迎留言给我。非常感谢。
