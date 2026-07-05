# FoodDrinkApp - 食物与热量追踪应用


## 项目概述


FoodDrinkApp 是一款基于 .NET MAUI 的跨平台移动应用，作为移动计算课程的期末作业开发。应用帮助用户追踪每日饮食、记录营养信息并监控热量摄入，采用 MVVM 架构模式设计。


## 主要功能


### 核心功能

- **食物管理**：支持添加、查看、删除食物记录，包含完整的营养信息（热量、蛋白质、碳水、脂肪）
- **热量追踪**：实时计算当日摄入总热量，通过进度条直观展示与目标（2000 kcal）的差距
- **营养分析**：自动计算蛋白质、碳水、脂肪三大营养素的供能比例
- **搜索功能**：支持按名称、分类、描述、标签进行实时模糊搜索
- **滑动删除**：左滑手势删除食物，带确认对话框防止误操作


### 硬件集成

- **摄像头**：调用设备相机拍摄餐食照片
- **GPS定位**：记录用餐地点，支持反向地理编码转换为可读地址
- **文字转语音**：语音朗读功能，提升无障碍体验
- **振动与触觉反馈**：操作确认的触感反馈


### 无障碍功能

- **深色模式支持**：跟随系统主题自动切换
- **动态字体缩放**：可调节字体大小，提升可读性
- **屏幕阅读器支持**：SemanticProperties 属性兼容 TalkBack


## 技术栈


| 类别 | 技术 |
|------|------|
| 框架 | .NET MAUI (.NET 9.0) |
| 架构 | MVVM (Model-View-ViewModel) |
| 数据库 | SQLite (sqlite-net-pcl) |
| 界面语言 | XAML |
| 支持平台 | Android 9.0+、Windows |


## 项目结构


```
FoodDrinkApp/
├── Models/              # 数据模型 (FoodItem.cs)
├── Views/               # XAML 页面 (MainPage, AddItemPage 等)
├── Services/            # 数据库、语音、无障碍等服务
├── Resources/           # 图片、字体、样式资源
├── App.xaml             # 应用全局资源
├── AppShell.xaml        # 导航外壳
└── MauiProgram.cs       # 应用入口
```


## 运行指南


### 环境要求

- Visual Studio 2022（含 .NET MAUI 工作负载）
- Android SDK（API 34 或更高）
- Android 模拟器或物理设备


### 克隆与运行

```bash
git clone https://github.com/chengzi-77/FoodDrinkApp.git
cd FoodDrinkApp
```

在 Visual Studio 中打开 `FoodDrinkApp.sln`，选择 Android 模拟器，按 `F5` 运行。


## 关键技术实现


### 数据库服务

`DatabaseService` 类统一管理 SQLite 数据库的初始化、种子数据填充、增删改查及搜索操作。数据持久化确保食物记录在应用重启后依然存在。


### 无障碍服务

`AccessibilityService` 递归遍历可视化树，对所有文字控件应用字体缩放，并缓存原始尺寸以便恢复。


### 硬件功能实现

- **摄像头**：`MediaPicker.Default.CapturePhotoAsync()`
- **定位**：`Geolocation.GetLocationAsync()` + `Geocoding.GetPlacemarksAsync()`
- **文字转语音**：`TextToSpeech.Default.SpeakAsync()`
- **触觉反馈**：`Vibration.Default.Vibrate()` + `HapticFeedback.Default.Perform()`


### 搜索与统计

支持多字段（名称、分类、描述、标签）实时模糊搜索，不区分大小写。自动计算当日热量进度和三大营养素的供能比例。
