#CSS 

**flex-grow**
在容器宽度不够分的情况下，元素会根据flex-grow来决定
定义容器成员的放大比例（容器宽度 > 子元素的总宽度时，如何伸展）
flex-grow默认是0，表示即使存在剩余空间，不会放大
如果容器成员的flex-grow 都是1 ，则他们会等分地使用剩余空间
如果其中一个容器成员的flex-grow属性为2，其他项目都为1，则前者占据的空间将比其他项多一倍
（flex-grow的值，可以理解为，当前容器成员需要占据剩余空间的相对比例：当前元素的flex-grow / 所有兄弟元素的flex-grow）


**flex-shrink**
定义了项目的缩小比例，默认为1，即如果空间不足，该容器成员将缩小
flex元素仅在默认宽度之和，大于容器的时候，才会发生收缩，其收缩的大小是依据flex-shrink的值
如果所有的容器成员的flex-shrink属性都为1，当空间不足时，都将等比例缩小
如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小

**flex-basis**
定义了初始大小，默认为auto
如果为0，则会根据内容撑开
flex-basis比width有搞更高的优先级

**flex**
flex: <flex-grew> <flex-shrink>? || <flex-basis>
flex: 1 = flex: 1 1 0%
flex: 2 = flex: 2 1 0%
flex: auto = flex: 1 1 auto
flex: none = flex: 0 0 auto


