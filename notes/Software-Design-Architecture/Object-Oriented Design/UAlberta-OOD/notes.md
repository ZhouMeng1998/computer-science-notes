### Module 1

#### 1.1.2 – Software Architect and Design Roles in Industry

> software architect与software design有什么区别？

software architect是对于一个需求提出solution，他要纵观全局，要知道用哪些技术，框架，数据库，分布式去实现这个需求，同时他能够设计出团队中的分工。简而言之，**他能为软件开发设计出一张图纸**。

![image-20201010111514991](C:\Users\Philip\AppData\Roaming\Typora\typora-user-images\image-20201010111514991.png)

software design是关注implementation，software architecture关注的是big picture

一个建筑如果没有好的建筑师师和土木工程师来设计，就很容易倒塌；**同理，一个大型软件如果没有好的架构和设计也会出一大堆问题。**再用建筑打个比方，现在西方的著名建筑，比如圣保罗教堂，万神殿，都是运用了柱式，拱等经久不衰的"建筑设计模式"，这样的建筑才经得起时间考验，才美。

architecture和design中最大的trade-off就是speed & quality，用户/management希望产品上线越快越好，开发团队则希望保证质量，开发出robust system

`simplicity`是一切design和architect的核心原则，吴军之前也讲过，能简化就不要复杂化

> architect roadmap

一开始都是从intern，new grad做起，随着项目经验不断丰富，你能驾驭的项目规模也越来越大，这时候你就慢慢往架构那方向靠了，所有的architect都是从engineer做起的

> communication

architect要懂得跟团队里不同的人如何去communicate，他既要很懂代码，又要懂商业，产品管理，也要懂测试运维，跟不同的人沟通方式是不一样的，比如跟management沟通，他们可不想听代码，他们只想听你的solution