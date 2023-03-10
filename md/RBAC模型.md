### 一、权限系统与RBAC模型概述
> RBAC(Role-Based Access Control) 基于角色的访问控制

* RBAC认为权限可以抽象为：`Who对What的How的访问操作`这个逻辑表达式是否为True的求解过程
  即将权限问题转化为Who、What、How的问题。who、what、how构成了访问权限三元组。
* RBAC支持公认的安全原则：最小特权原则、责任分离原则和数据抽象原则

> RBAC96是一个模型族，其中包括RBAC0~RBAC3四个概念性模型

1. 基本模型RBAC0定义了完全支持RBAC概念的任何系统的最低需求。

2. RBAC1和RBAC2两者都包含RBAC0，但各自都增加了独立的特点，它们被称为高级模型。

3. RBAC1中增加了角色分级的概念，一个角色可以从另一个角色继承许可权。

4. RBAC2中增加了一些限制，强调在RBAC的不同组件中在配置方面的一些限制。

5. RBAC3称为统一模型，它包含了RBAC1和RBAC2，利用传递性，也把RBAC0包括在内。这些模型构成了RBAC96模型族。

###　二、RBAC模型简述

> RBAC0定义了能构成一个RBAC控制系统的最小的元素集合

* 在RBAC之中,包含用户users(USERS)、角色roles(ROLES)、目标objects(OBS)、操作operations(OPS)、许可权permissions(PRMS)五个基本数据元素，此模型指明用户、角色、访问权限和会话之间的关系。
* 每个角色至少具备一个权限，每个用户至少扮演一个角色
* 可以对两个完全不同的角色分配完全相同的访问权限
* 会话由用户控制，一个用户可以创建会话并激活多个用户角色，从而获取相应的访问权限，用户可以在会话中更改激活角色，并且用户可以主动结束一个会话
* 用户和角色是多对多的关系，表示一个用户在不同的场景下可以拥有不同的角色。

> RBAC1，基于RBAC0模型

* 引入角色间的继承关系，即角色上有了上下级的区别，角色间的继承关系可分为一般继承关系和受限继承关系
* 一般继承关系仅要求角色继承关系是一个绝对偏序关系，允许角色间的多继承。而受限继承关系则进一步要求角色继承关系是一个树结构，实现角色间的单继承
* 这种模型合适于角色之间的层次明确，包含明确

> RBAC2，基于RBAC0模型

* 引入了角色的访问控制，RBAC2模型中添加了责任分离关系。RBAC2的约束规定了权限被赋予角色时，或角色被赋予用户时，以及当用户在某一时刻激活一个角色时所应遵循的强制性规则。责任分离包括静态责任分离和动态责任分离。约束与用户-角色-权限关系一起决定了RBAC2模型中用户的访问许可，此约束有多种。

1. 互斥角色 ：同一用户只能分配到一组互斥角色集合中至多一个角色，支持责任分离的原则。互斥角色是指各自权限互相制约的两个角色。对于这类角色一个用户在某一次活动中只能被分配其中的一个角色，不能同时获得两个角色的使用权。
2. 基数约束 ：一个角色被分配的用户数量受限；一个用户可拥有的角色数目受限；同样一个角色对应的访问权限数目也应受限，以控制高级权限在系统中的分配。
3. 先决条件角色 ：可以分配角色给用户仅当该用户已经是另一角色的成员；对应的可以分配访问权限给角色，仅当该角色已经拥有另一种访问权限。指要想获得较高的权限，要首先拥有低一级的权限。
4. 运行时互斥 ：例如，允许一个用户具有两个角色的成员资格，但在运行中不可同时激活这两个角色。

> RBAC3,最全面、最复杂的权限管理，它是基于RBAC0的基础上，将RBAC1和RBAC2进行整合了

> RBAC模型的优缺点

* RBAC模型没有提供操作顺序控制机制。这一缺陷使得RBAC模型很难应用关于那些要求有严格操作次序的实体系统。
* RBAC的核心是用户只和角色关联，而角色代表对了权限，这样设计的优势在于使得对用户而言，只需角色即可以，而某角色可以拥有各种各样的权限并可继承。