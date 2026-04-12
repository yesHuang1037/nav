## 📋 项目结构解读

这是一个 **ROS 2 自主导航机器人系统** 项目。以下是核心架构：

### 🏗️ 项目组成（8个功能模块）

| 模块 | 功能 | 关键文件 |
|------|------|--------|
| **path_searching** | 路径规划（A*算法 + ESDF） | Astar.cpp, esdf_map.cpp, plan_manager.cpp |
| **mpc_follower** | 轨迹跟踪控制（模型预测控制） | mpc_controller.cpp, robot_model.h |
| **goal_pub** | 目标点发布 | multigoal_pub.cpp |
| **navigoal_manager** | 导航目标管理 | manager.cpp |
| **path_following** | 路径跟踪执行 | PathFollower.cpp |
| **detect_obs** | 障碍物检测 | obstacle_processor.cpp |
| **vel_forwarder** | 速度命令转发 | forwarder.cpp |
| **test_car** | 测试/仿真车辆 | TrajFollower.cpp |

### 🔄 数据流向

```
目标点 (goal_pub)
    ↓
导航管理 (navigoal_manager)
    ↓
路径规划 (path_searching - A* + ESDF)
    ↓
路径跟踪 (path_following)
    ↓
MPC控制器 (mpc_follower)
    ↓
速度转发 (vel_forwarder)
    ↓
执行器 (test_car)
    
障碍信息 (detect_obs) → 输入到规划和控制模块
```

---

## 🚀 入门上手建议

### 1️⃣ **快速编译和运行**
```bash
# 编译所有模块
colcon build

# 编译特定模块（推荐新手先单独编译）
colcon build --packages-select path_searching
colcon build --packages-select mpc_follower
```

### 2️⃣ **理解关键组件** （从简到难）

- **从 goal_pub 开始** ✅ 最简单
  - 负责发布目标点：multigoal_pub.cpp
  - 查看配置：goalpub_param.yaml
  
- **了解路径规划** 🔶 中等难度
  - A*算法实现：Astar.h, Astar.cpp
  - ESDF距离场：esdf_map.cpp
  - 📖 调试指南在 README.md 中有详细说明（ESDF验证步骤）

- **学习控制器** 🔴 较难
  - MPC控制实现：mpc_controller.cpp
  - 机器人模型：robot_model.h
  - 配置参数：mpc_params.yaml

### 3️⃣ **文件夹用途说明**

```
d:\navigation
├── src/              ← 源代码（8个ROS2包）
├── launch/           ← 启动脚本
├── cfg/              ← 参数配置文件（YAML）
├── build/            ← 编译生成目录
├── install/          ← 安装生成目录
└── log/              ← 构建日志
```

### 4️⃣ **推荐学习路径**

1. **阅读README** - 了解ESDF调试流程
2. **查看launch文件** - 理解各模块如何启动和参数加载
3. **研究配置文件** (`.yaml`) - 了解可调参数
4. **阅读头文件** (`.h`) - 理解数据结构和接口
5. **阅读源文件** (`.cpp`) - 理解具体实现逻辑

### 5️⃣ **常见任务建议**

- 🔧 **调试路径规划**：使用 `esdf_benchmark` 工具验证距离场计算
- ⚙️ **调整控制参数**：修改各包中的 `cfg/` 目录下的YAML文件
- 🎯 **设置目标点**：编辑 goalpub_param.yaml
- 📊 **可视化调试**：使用RViz查看路径规划结果

### 6️⃣ **关键文档位置**
- 路径搜索说明：esdf_instruction.md
- MPC基准测试：1.md
- 主题列表：topiclist.md

---

需要帮你深入某个特定模块或解答具体问题吗？