## Week 1 Union Find

### 1 Quick Find

![image-20201021113906754](https://raw.githubusercontent.com/ZhouMeng1998/IMG/image-upload/20201021113907.png)

If they have the same id, then they are connected. For example, 0 ,5 and 6 are connected

> Union操作

change all entries whose id equals id[p] to id[q]，如果数据很多，这种Union操作效率很低，因为有大量的数据要修改

> Implementation：

![image-20201021113958833](https://raw.githubusercontent.com/ZhouMeng1998/IMG/image-upload/20201021113959.png)



