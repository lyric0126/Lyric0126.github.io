## 项目
---
<div style="display: flex; align-items: center; gap: 24px; margin-bottom: 2rem;">
  <img src="static/assets/img/raft.png" alt="raftstereo_quant" style="width: 360px; height: auto; border-radius: 6px;">
  <div style="line-height: 1.6;">
    <h4 style="margin: 0;">RAFT-Stereo 模型的 QAT/PTQ 量化、张量RT部署与 Orin 性能瓶颈优化</h4>
    <p><strong>作者：</strong>刘少坤（HPC && AI Infer INTERN）<br>
    <strong>性质：</strong>模型加速 · 边缘端推理优化项目<br>
    <strong>工具：</strong>PyTorch、TensorRT、CUDA、Nsight Systems、QAT/PTQ、TensorRT Pluging<br>
    <strong>简介：</strong>负责<strong>RAFT-Stereo 端侧量化、推理加速与 Orin 上的性能重构</strong>。基于 <strong>QAT + PTQ 混合量化策略</strong>，构建 <strong>特征提取网络的对称量化</strong>、<strong>GRU recurrent block 的非均匀量化
    <br><br>
    使用 <strong>Nsight Systems / Nsight Compute</strong> 对推理过程进行热点定位，发现计算瓶颈主要集中于：  
    • <strong>Cost Volume 构建中的 3D Gather / Correlation</strong>  
    • <strong>GRU 门控循环的序列依赖</strong>  
    • <strong>双线性采样（grid_sample）算子的大量 global memory 访问</strong>  
    • <strong>部分卷积层的 kernel launch overheading</strong>  
    <br><br>
    针对这些瓶颈，设计并实现多项优化：  
    • <strong>GRU kernel 融合（gate fusion）</strong>，将多个 matmul+activation 合并为单 kernel，减少 launch 次数  
    • <strong>量化后卷积层的 TensorRT 层融合</strong>（Conv + BN + ReLU）  
    • <strong>重排特征图 layout</strong>，减少冗余 global memory 访问  
    • <strong>基于cuda graph策略</strong>，提升量化算子吞吐  
    </p>
  </div>
</div>

---
<div style="display: flex; align-items: flex-start; gap: 24px; margin-bottom: 2rem;">
  <div style="display: flex; flex-direction: column; gap: 16px;">
    <img src="static/assets/img/robot.png" alt="pipeline" style="width: 360px; height: auto; border-radius: 6px;">
    <img src="static/assets/img/output.gif" alt="motion-demo" style="width: 360px; height: auto; border-radius: 6px;">
  </div>

  <div style="line-height: 1.6;">
    <h4 style="margin-top: 0;">面向人形机器人的视频驱动动作学习系统架构与工程化实现</h4>
    <p>
      <strong>作者：</strong>刘少坤（核心系统设计与实现）<br>
      <strong>性质：</strong>具身智能 / 机器人学习系统工程项目<br>
      <strong>工具：</strong>PyTorch，Python，SMPL-X，GVHMR，GMR，Isaac Lab，Unitree G1
    </p>
    <p>
      从系统工程视角构建了一套<strong>视频 → 人体运动 → 机器人关节轨迹 → 全身控制策略</strong>的端到端动作学习流水线。
      系统采用<strong>模块化、分阶段解耦架构</strong>，统一人体运动中间表示与数据接口，
      支持人体动作恢复、跨形态动作重定向及下游策略训练的灵活组合与扩展。
      本人主导完成<strong>系统架构设计、模块接口规范、数据管线搭建与关键组件工程化集成</strong>，
      并针对长序列动作中的稳定性与一致性问题进行优化。
      实验验证表明，该系统能够基于单目视频稳定生成符合机器人运动学约束的关节级时序数据，
      并直接用于全身运动跟踪策略训练，具备<strong>低成本数据驱动人形机器人技能构建</strong>的工程可行性。
    </p>
  </div>
</div>

---

<div style="display: flex; align-items: center; gap: 24px; margin-bottom: 2rem;">
  <img src="static/assets/img/biyesheji.png" alt="biyesheji" style="width: 360px; height: auto; border-radius: 6px;">
  <div style="line-height: 1.6;">
    <h4 style="margin: 0;">基于FPGA加速的LSTM中的数据优化研究</h4>
    <p><strong>作者：</strong>刘少坤（独立项目）<br>
    <strong>性质：</strong>本科毕业设计<br>
    <strong>工具：</strong>PyTorch，Python，NumPy，Pandas，Matplotlib<br>
    <strong>简介：</strong>构建自定义<strong>LSTM模型</strong>并在<strong>PyTorch</strong>中完成训练，重点实现<strong>TOP-K剪枝</strong>与<strong>对数量化</strong>方法，有效压缩模型参数量，提升硬件部署效率。通过多组实验调参，成功将模型<strong>准确率控制在94%以上</strong>的同时，实现<strong>1.35×推理加速</strong>。本人独立完成<strong>数据处理、剪枝逻辑实现、量化代码设计与精度验证</strong>。</p>
  </div>
</div>

---

<div style="display: flex; align-items: center; gap: 24px; margin-bottom: 2rem;">
  <img src="static/assets/img/eda_chuangxin.png" alt="eda_project" style="width: 360px; height: auto; border-radius: 6px;">
  <div style="line-height: 1.6;">
    <h4 style="margin: 0;">组合逻辑环路振荡分析与逻辑重构（EDA创芯大赛）</h4>
    <p><strong>作者：</strong>刘少坤（算法负责人）<br>
    <strong>性质：</strong>EDA精英挑战赛 · 决赛项目<br>
    <strong>工具：</strong>C++，VPI，SAT求解，QM逻辑最小化，Tarjan，DFS<br>
    <strong>简介：</strong>主导构建<strong>环路识别与振荡判断算法</strong>，采用<strong>Tarjan算法</strong>提取<strong>强连通子图</strong>，结合<strong>查找表</strong>替代哈希映射实现<strong>邻接表构建加速</strong>。设计<strong>多类拓扑结构识别</strong>与<strong>条件回溯规则</strong>，辅助<strong>自洽性分析</strong与<strong>QM逻辑重构</strong>，保证<strong>功能等价</strong>与<strong>环路消除</strong>。</p>
  </div>
</div>

---

<div style="display: flex; align-items: center; gap: 24px; margin-bottom: 2rem;">
  <img src="static/assets/img/project1.png" alt="nasal swab robot" style="width: 360px; height: auto; border-radius: 6px;">
  <div style="line-height: 1.6;">
    <h4 style="margin: 0;">基于CNN与ROS的智能核酸采样机器人</h4>
    <p><strong>作者：</strong>刘少坤（图像识别与AI算法模块负责人）<br>
    <strong>性质：</strong>智慧医疗创新项目<br>
    <strong>工具：</strong>TensorFlow Lite / K210，CNN图像分类，ROS1，MoveIt，SLAM，PID控制，STM32，ESP32<br>
    <strong>简介：</strong>该系统基于<strong>CNN模型</strong>实现<strong>手势与身份图像识别</strong>，部署于<strong>K210边缘计算芯片</strong>，实现用户触发采样识别。使用<strong>ROS</strong>搭建<strong>六轴机械臂</strong>与<strong>移动底盘</strong>的控制架构，完成<strong>核酸拭子抓取、采样与消毒全过程</strong>，并结合<strong>Cartographer建图</strong>与<strong>AMCL定位</strong>完成<strong>全自主路径规划与语音播报</strong>。项目融合<strong>AI视觉感知</strong>与<strong>机器人运动控制</strong>，为智慧防疫提供智能解决方案。</p>
  </div>
</div>
