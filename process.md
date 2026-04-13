## 1.goal_pub
编译goal_pub模块
运行结果：加载目标点，发布一个目标点，原因检测不到距离变换

## 2.navigoal_manager
编译navigoal_manager模块
问题：1.头文件缺少UInt16MultiArray
解决：添加头文件
2.main在namespace中报错

作用：订阅上一位姿势，根据姿势发布目标点
