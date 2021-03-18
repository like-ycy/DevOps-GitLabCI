# 03-GitLabCI VS Jenkins



`Jenkins` 是一个广泛用于持续集成的可视化 `web` 自动化工具，`jenkins` 可以很好的支持各种语言的项目构建，也完全兼容`ant`、`maven`、`gradle`等多种第三方构建工具，同时跟`svn`、`git`能无缝集成，也支持直接与知名源代码托管网站，比如`github`、`bitbucket`直接集成，而且插件众多，在这么多年的技术积累之后，在国内大部分公司都有使用`Jenkins`。



`gitlab-CI`是`gitlab8.0`之后自带的一个持续集成系统，中心思想是当每一次`push`到`gitlab`的时候，都会触发一次脚本执行，然后脚本的内容包括了测试，编译，部署等一系列自定义的内容。

`gitlab-CI`的脚本执行，需要自定义安装对应`gitlab-runner`来执行，代码`push`之后，`webhook`检测到代码变化，就会触发`gitlab-CI`，分配到各个`Runner`来运行相应的脚本`script`。这些脚本有的是测试项目用的，有的是部署用的。



## 差异点对比



**分支的可配置性**

- 使用GitLab CI，新创建的分支无需任何进一步配置即可立即使用CI管道中的已定义作业。
- Jenkins 2 基于gitlab的多分支流水线可以实现。相对配置来说gitlab更加方便一些。



**定时执行构建**

有时，根据时间触发作业或整个管道会有所帮助。例如，常规的夜间定时构建。

- 使用Jenkins 2可以立即使用。可以在应执行作业或管道的那一刻以cron式语法定义。

- GitLab CI没有此功能。但是，可以通过一种变通办法来实现：通过WebAPI使用同一台或另一台服务器上的cronjob触发作业和管道。

  

尽管使用GitLab CI无法做到这一点，其实如果配置了提交代码即触发流水线，那么最后一次提交的构建在什么时候没有什么不同，反而减少未提交代码的定时构建资源浪费。



**拉取请求支持**

如果很好地集成了存储库管理器和CI / CD平台，您可以看到请求的当前构建状态。使用这种功能，可以避免将代码合并到不起作用或无法正确构建的主分支中。

- Jenkins没有与源代码管理系统进一步集成，需要管理员自行写代码或者插件实现。
- GitLab与其CI平台紧密集成，可以方便查看每个打开和关闭拉动请求的运行和完成管道。



**权限管理**

从存储库管理器继承的权限管理对于不想为每个服务分别设置每个用户的权限的大型开发人员或组织团体很有用。大多数情况下，两种情况下的权限都是相同的，因此默认情况下应将它们配置在一个位置。

- 由于GitLab与GitLabCI的深度整合，权限可以统一管理。

- 由于Jenkins 2没有内置的存储库管理器，因此它无法直接在存储库管理器和CI / CD平台之间合并权限。





**存储库交互**

- GitLab CI是Git存储库管理器GitLab的固定组件，因此在CI / CD流程和存储库功能之间提供了良好的交互。
- Jenkins 2与存储库管理器都是松散耦合的，因此在选择版本控制系统时它非常灵活。此外，就像其前身一样，Jenkins 2强调了对插件的支持，以进一步扩展或改善软件的现有功能。





**插件管理**

- 扩展Jenkins的本机功能是通过插件完成的。插件的维护，保护和升级成本很高。
- GitLab是开放式的，任何人都可以直接向代码库贡献更改，一旦合并，它将自动测试并维护每个更改。





---





## 优势与劣势



**GitLabCI**

- 轻量级，不需要复杂的安装手段。
- 配置简单，与`gitlab`可直接适配。
- 实时构建日志十分清晰，`UI`交互体验很好
- 使用 `YAML` 进行配置，任何人都可以很方便的使用。

- 没有统一的管理界面，无法统筹管理所有项目
- 配置依赖于代码仓库，耦合度没有`Jenkins`低



**Jenkins**

- 编译服务和代码仓库分离，耦合度低
- 插件丰富，支持语言众多。
- 有统一的`web`管理界面。
- 插件以及自身安装较为复杂。
- 体量较大，不是很适合小型团队。





## 实际应用



- GitLabCI 有助于DevOps人员，例如敏捷开发中，开发与运维是同一个人，最便捷的开发方式。
- JenkinsCI适合在多角色团队中，职责分明、配置与代码分离、插件丰富。


