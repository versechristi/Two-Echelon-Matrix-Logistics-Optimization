# 物流路径优化系统 (Logistics Optimization System)

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

这是一个针对**多站点、二级车辆路径问题（MD-2E-VRPSD）** 设计的综合性物流优化桌面应用。系统深度集成了**无人机协同配送**与**拆分订单交付**两大现代物流场景，并通过一个功能丰富的图形用户界面（GUI）提供给用户。用户可以轻松配置问题参数、选择优化算法、执行优化流程并对结果进行多维度的可视化分析。

该系统的核心应用场景为：一个或多个物流中心（Depot）负责向多个销售网点（Outlet）进行补货（第一级运输），随后，销售网点作为二级枢纽，利用**货车和无人机**共同为终端客户完成“最后一公里”的配送（第二级运输）。

## 系统界面与核心功能演示

系统提供了高度集成且用户友好的图形界面，将复杂参数配置、算法执行与结果可视化融为一体。

![24c4676c66dd8844b5e4303636b804f4](https://github.com/user-attachments/assets/09363806-95e5-4d14-aed2-032c594be7c5)

* **左侧为控制面板**：集成了参数配置区（数据生成、载具属性、目标函数、算法参数）和执行控制区（数据生成、算法选择、运行优化）。
* **右侧为结果展示面板**：通过选项卡清晰地展示交互式地图、算法迭代曲线、性能对比图和详细的文本报告。

---

### 结果可视化效果

#### 1. 交互式地理路径图

优化完成后，系统利用 `Folium` 库生成详细的交互式HTML地图，用户可以在浏览器中进行缩放、平移、点击等操作，直观地审查路径规划的每一个细节。

![f749df2b40efa8b0afae3704661983d9](https://github.com/user-attachments/assets/862e4452-c834-455b-b6c9-f4165e84de60)

> **图例说明**：
> * **深蓝色方块**: 一级物流中心 (Depot)
> * **绿色圆形**: 二级销售网点 (Outlet)
> * **橙色图钉**: 终端客户 (Customer)
> * **粗实线**: 第一级运输路径（货车从物流中心到销售网点）
> * **细实线**: 第二级车辆运输路径（货车从销售网点到客户）
> * **虚线**: 第二级无人机配送路径

#### 2. 算法性能对比图

为了方便横向比较不同算法的优劣，系统提供了直观的条形对比图，从“总成本”和“仿真实现时间”两个关键维度对结果进行评估。

![5415bc38f44f823ab85defdc074a5117](https://github.com/user-attachments/assets/47f009b1-1a13-4ca9-a7c6-8c28840a20be)
![213e76ff12149d24c0084b2624216398](https://github.com/user-attachments/assets/0884c366-5b0d-43db-8824-67063089c617)

> **图例说明**：
> * **左图 (Weighted Cost)**：对比了贪心、遗传、模拟退火和粒子群四种算法在加权目标函数（综合了运输成本、时间成本和惩罚项）上的最终得分。成本越低，代表解决方案质量越高。
> * **右图 (Makespan)**：展示了各个算法仿真完整实现需要的时间，反映了算法的优化能力。

---

## 核心功能特点

* **高级问题建模**
    * **二级网络 (Two-Echelon)**：完整模拟从中心仓库到二级网点，再到终端客户的两级配送网络。
    * **多仓库支持 (Multi-Depot)**：支持从多个一级物流中心出发，优化更复杂的区域物流网络。
    * **无人机协同 (Drone Collaboration)**：允许车辆与无人机并行工作，无人机从销售网点出发，执行短途、小批量包裹的配送任务。
    * **拆分配送 (Split Deliveries)**：允许一个客户的需求由多次配送（来自不同车辆或无人机）共同满足，以提高整体装载率和效率。

* **强大的算法套件**
    * **遗传算法 (Genetic Algorithm, GA)**：基于生物进化原理的全局搜索启发式算法。
    * **模拟退火 (Simulated Annealing, SA)**：基于物理退火过程的概率性局部搜索算法。
    * **粒子群优化 (Particle Swarm Optimization, PSO)**：模拟鸟群觅食行为的群体智能优化算法。
    * **贪心启发式 (Greedy Heuristic)**：一种快速、直接的构造性启发式算法，可用于生成基准解。

* **全功能图形用户界面 (GUI)**
    * **线程安全**：优化计算在独立的后台线程中执行，确保了用户界面的流畅和响应性，避免了长时间计算导致的界面卡死。
    * **参数化配置**：通过直观的选项卡界面，用户可以自定义所有关键参数，包括数据生成、载具属性、目标函数权重和各算法的超参数。
    * **配置持久化**：支持将当前的所有参数配置保存到 `.ini` 文件中，也支持从文件中加载配置，方便重复实验和分享设置。
    * **实时状态反馈**：通过底部的状态栏实时显示程序当前状态，如“数据生成中...”、“正在运行优化...”、“优化完成”等。

* **深度结果可视化与分析**
    * **交互式地理地图**：利用 `Folium` 生成可在浏览器中打开的交互式HTML地图。
    * **算法迭代曲线**：使用 `Matplotlib` 实时绘制算法在迭代过程中的目标函数值（成本）收敛曲线。
    * **多算法性能对比**：通过条形图清晰地对比不同算法在“总成本”和“计算时间”两个关键指标上的最终表现。
    * **详细文本报告**：为每个算法的优化结果生成详细的文本报告。
    * **结果导出**：所有生成的图表（迭代图、对比图）和报告均可一键保存到本地。

* **灵活的数据管理**
    * **内置数据生成器**：可根据用户设定的中心点、网点和客户数量、地理半径、需求范围等参数，快速生成用于测试的模拟数据。
    * **标准格式兼容**：提供了 `Solomon` 标准数据集的解析器框架，具备扩展以支持标准VRPTW benchmark的能力。

## 项目结构

```
logistics_optimization/
│
├── main.py                  # 主程序入口，负责初始化环境并启动 GUI
├── requirements.txt         # 项目依赖库列表
├── README.md                # 项目说明文件
│
├── config/                  # 配置文件目录
│   └── default_config.ini   # 参数默认配置文件
│
├── core/                    # 核心业务逻辑与计算模块
│   ├── cost_function.py     # 目标函数（成本、时间、惩罚项）计算模块
│   ├── distance_calculator.py # 地理距离（Haversine）计算工具
│   ├── problem_utils.py     # 问题核心工具（解决方案定义、邻域操作等）
│   └── route_optimizer.py   # 优化流程编排器，调用算法并整合结果
│
├── data/                    # 数据生成与加载模块
│   ├── data_generator.py    # 合成数据生成器
│   └── solomon_parser.py    # Solomon 标准数据集解析器
│
├── algorithm/               # 优化算法实现模块
│   ├── genetic_algorithm.py # 遗传算法实现
│   ├── simulated_annealing.py # 模拟退火算法实现
│   ├── pso_optimizer.py     # 粒子群优化算法实现
│   └── greedy_heuristic.py  # 贪心启发式算法实现
│
├── gui/                     # 图形用户界面模块
│   └── main_window.py       # GUI主窗口，负责所有用户交互和流程控制
│
├── visualization/           # 结果可视化模块
│   ├── map_generator.py     # Folium 交互式地图生成器
│   └── plot_generator.py    # Matplotlib 图表（迭代、对比）生成器
│
└── output/                  # 输出目录，存放运行结果
```


## 安装与运行

1.  **克隆仓库**
    ```bash
    git clone <your-repository-url>
    cd logistics_optimization
    ```

2.  **创建并激活虚拟环境 (推荐)**
    ```bash
    # Windows
    python -m venv venv
    venv\Scripts\activate

    # Linux/macOS
    python -m venv venv
    source venv/bin/activate
    ```

3.  **安装依赖**
    根据 `requirements.txt` 文件，安装所有必需的库：
    ```bash
    pip install -r requirements.txt
    ```

4.  **启动程序**
    在项目根目录下运行 `main.py` 即可启动图形用户界面：
    ```bash
    python main.py
    ```

## 使用指南

1.  **参数配置 (左侧面板)**:
    * 在 **"Data Generation"** 标签页设置数据生成参数（中心点、网点、客户数量等）。
    * 在 **"Vehicle"** 和 **"Drone"** 标签页分别设置货车和无人机的属性（载重、速度、成本、无人机续航等）。
    * 在 **"Objective"** 标签页通过滑块或输入框调整成本和时间在目标函数中的权重，并设定未满足需求的惩罚值。
    * 在下方的 **算法参数区** (GA, SA, PSO) 配置所选算法的特定参数（如种群大小、迭代次数、冷却速率等）。

2.  **生成/加载数据**:
    * 点击 **"Generate Data"** 按钮生成模拟数据。
    * 点击 **"Load Config"** 可以从 `.ini` 文件加载之前保存的所有参数。

3.  **运行优化**:
    * 在 **"Algorithm Selection & Execution"** 区域勾选一个或多个需要运行和对比的算法。
    * 点击 **"Run Optimization"** 按钮开始执行。

4.  **查看与分析结果 (右侧面板)**:
    * **Route Map** 标签页：
        * 通过下拉菜单选择不同算法的结果。
        * 点击 **"Open Selected Map"** 按钮，在浏览器中查看对应算法的详细路径规划交互式地图。
    * **Iteration Curves** 标签页：查看各算法在优化过程中的成本收敛曲线图。
    * **Comparison** 标签页：查看各算法最终结果（加权成本、计算时间）的条形对比图。
    * **Detailed Report** 标签页：通过下拉菜单选择，查看对应算法的纯文本详细报告。
    * 所有图表和报告都可以通过下方的 "Save Plot" 或 "Save Report" 按钮进行保存。

## 主要依赖库

* **Tkinter** (Python 标准库): 用于构建图形用户界面。
* **Matplotlib**: 用于绘制静态路径图、迭代曲线图和对比图。
* **Folium**: 用于生成交互式 HTML 地图。
* **NumPy**: 用于高效的数值计算。

---
*本项目由Mr VerseChristi编写完成,若有疑问或者需要提供数据可以联系versechristi@gmail.com*
