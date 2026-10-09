HJC GeoPilot Pro 使用教程
Developed by Hjc · 由 Hjc 开发
iOS Location & Route Simulation Toolkit
本教程按“安装 → 离线熟悉 → 设计路线 → 模拟 → 连接设备 → 故障排查”的顺序说明。软件按钮名称保留英文，方便你在界面中查找。
本软件用于开发者测试自己拥有或获准测试的应用。第一次使用请保持 Offline preview（离线预览）开启。不要将本工具用于绕过第三方应用的反作弊、传感器校验或完整性检测。

1. 安装并启动
当前交付的是源码项目，不是可直接双击的 EXE。Windows 10/11 x64 首次运行需要安装 Python 和项目依赖。
1. 下载并解压 HJC-GeoPilot-Pro-Source.zip。不要在压缩包预览窗口内运行。
2. 安装 Python 3.12 x64。Python 3.12.15 是源码发布，不含 Windows 安装程序；可用的 3.12 Windows 安装程序是 3.12.10：Python 3.12.10 官方页面。
3. 在页面的 Files 列表中点击 Windows installer (64-bit)。运行安装程序时勾选 Add python.exe to PATH，并保留 Python Launcher。
4. 安装完成后，关闭并重新打开项目文件夹。
5. 双击 setup.bat。首次安装会联网下载 PySide6、pymobiledevice3、pyproj 等依赖。等待窗口显示 Setup completed。
6. 双击 run.bat 启动软件。以后通常只需双击 run.bat。若依赖安装中断，再运行 setup.bat。
项目使用 Python 3.12 创建独立的 .venv 环境。已有 Python 3.14 不必卸载；不要直接用其他 Python 版本运行 app.py。安装依赖需要网络，首次设置可能需要几分钟。
2. 首次启动与页面
左侧导航页面如下：
- Home：运行仪表盘、路线缩略图和 START / PAUSE / RESUME / STOP。
- Devices：USB 设备发现、连接状态与服务状态。
- Map：地图搜索、工作区位置和路线点编辑。
- Track Designer：按米制参数生成标准跑道。
- Route Editor：自由路线编辑、导入导出、撤销重做。
- Simulation：速度、圈数、起点、插值方式和实时数据。
- Manual Control：坐标输入、地图点击和键盘步进。
- Presets：场地保存、搜索、收藏、导入导出。
- Diagnostics：环境与设备诊断。
- Logs：查看、复制和导出运行日志。
- Settings：主题、速度单位、工作区恢复和数据目录。
窗口顶部的 TARGET 用于选择当前目标。Offline preview 默认勾选，此时程序只在电脑上预览和计算路线，不向手机发送定位指令。建议先用离线预览熟悉路线编辑和模拟。
窗口底部和 About 页面显示 HJC GeoPilot Pro、Developed by Hjc、由 Hjc 开发。
 
3. 地图与坐标
3.1 搜索地点或输入经纬度
进入 Map 页面，在搜索框输入地点名称，点击 Search。在线搜索需要网络。结果出现在旁边的下拉框，选择结果后地图会移动到该位置。
也可以直接输入纬度, 经度，例如：
28.68, 115.98
纬度在前，经度在后；英文逗号或中文逗号均可。直接输入坐标不依赖地点搜索服务。
软件输入、输出和设备指令使用 WGS84 坐标。高德 GCJ-02 或百度 BD-09 坐标不能直接当作 WGS84 使用，否则地图标记会偏移。示例场地不是经核实的校园坐标；请在地图上自行选取真实位置。
3.2 地图操作
- 鼠标滚轮：缩放。
- 按住鼠标拖动空白地图：平移。
- 鼠标移动到地图上：页面下方显示光标位置经纬度。
- Copy coordinates：复制当前光标坐标。
- Fit route：缩放到当前路线范围。
- Retry tiles：底图加载失败后重试。
- Normal：普通地图；Satellite：卫星图；Route：突出路线的地图。
在线地图不可用时，仍可用坐标网格、路线编辑和坐标输入。底图和地点搜索需要网络服务可达。
3.3 Map 页面点击动作
Map 页面可选择点击地图后的动作：
- Set workspace position：设置工作区位置，绿色标记随之移动。
- Add route point：在当前路线末尾添加一个路线点。
Map 页面主要用于编辑工作区位置。Manual Control 页面地图点击/拖动会执行手动定位操作；Simulation 页面显示模拟位置和已走轨迹。三者用途不同，请留意当前页面和顶部 TARGET。
4. 创建和编辑自由路线
进入 Route Editor。地图点击可增加路线点；拖动地图上的点可修改位置；右键路线点可删除。点位列表显示顺序和经纬度，可拖动列表重排，也可选中点后用 ↑ / ↓ 调整。
 
4.1 在地图上画路线
1. 先把地图平移、缩放到目标区域；必要时先在 Map 页面搜索地点。
2. 在 Route Editor 地图上按行进顺序依次点击路线位置。每次点击都会在末尾增加一个点。
3. 拖动点位微调；右键删除错误点。
4. 检查点位列表。第一点是起点，最后一点是终点。
5. 查看路线统计，确认点数、总长度、预计时间和 Open / Closed 状态。
6. Ctrl+Z 撤销，Ctrl+Y 重做；也可点击 Undo / Redo。
4.2 生成几何路线
Route Editor 的形状工具支持 Line、Rectangle、Circle、Ellipse：
1. 先把绿色工作区位置放到形状中心。
2. 选择形状，填写长轴/直径、短轴和旋转角度。
3. 点击 Generate shape。
4. 生成后可继续拖点、删除点和调整顺序。
Line 是开放路线；矩形、圆形和椭圆形默认闭合。尺寸按米计算，程序在局部米制坐标中生成形状，再转换为经纬度。
4.3 路线编辑按钮
- Open / Close：切换路线是否闭合。闭合路线会连接末点和首点。
- Reverse：反转点顺序，改变行进方向。
- Smooth：样条平滑路线。它可能使路线超出控制点范围，生成后务必在地图检查；不满意可 Undo。
- Clear：清空当前路线。
- Duplicate：复制路线并进入另存流程。
- Rename：重命名路线。
- Delete selected：删除列表中选中的点。
- Save / Save as：导出路线文件。
修改会自动保存到工作区。若要得到独立文件，使用 Save / Save as。
4.4 导入和导出
点击 Import JSON / GPX 选择路线文件；点击 Save / Save as 导出 JSON 或 GPX。
JSON 包含路线名称、版本、作者、创建时间、坐标系、点、速度配置和元数据；导出作者为 Hjc。GPX 适合交换轨迹点，但不保存所有 JSON 扩展信息，例如分段速度配置。
导入前请确认坐标系为 WGS84。含有多个互不相连轨迹段的 GPX 会被拒绝，避免程序把轨迹段错误连接起来。请先在原软件中拆分轨迹。
5. 生成标准田径场
进入 Track Designer。它按局部 ENU 米制坐标生成“两段直道 + 两个半圆”，再转换回 WGS84。
 
5.1 快速生成约 400 米跑道
1. 在地图找到跑道中心。可点击地图或拖动绿色标记。
2. 点击 400 m geometry。程序按两段直道加两个半圆的几何公式生成约 400 米周长。
3. 检查路线是否覆盖实际跑道。
4. 调整 Rotation 设置方向。0° 表示长轴朝东，角度逆时针增加。
5. 设置 Laps 圈数，再点击 Generate / Apply。
6. 查看单圈距离、总距离、预计时间和点数。
默认半径约 36.8 米，直道约 84.4 米。不同跑道的测量线、分道和起跑线可能不同；此功能是几何模型，不是赛事测量认证。请用卫星图核对跑道位置和形状。
5.2 自定义参数
Dimensions 可选：
- Straight + Radius：输入直道长度和弯道半径。
- Long axis + Short axis：输入长轴和短轴。
长轴不能小于短轴。修改中心、角度、圈数或尺寸后，地图和距离统计会更新。拖动跑道中心可整体移动路线。路线生成后成为当前工作路线，可到 Simulation 配置速度和运行。
6. 路线运动模拟
6.1 设置参数
进入 Simulation 页面：
- Speed / Pace：输入速度，可选 m/s、km/h、min/km。
- Laps：运行圈数。闭合路线按圈运行；开放路线重复时会往返。
- Start / Jump point：从第几个路线点开始，序号从 1 开始。
- Reverse：反向运行。
- Linear：线性插值。
- Spline：样条平滑并重采样。此模式从第 1 点开始；若要指定起点，可先在 Route Editor 平滑并检查路线，再回到 Simulation 选择起点。
- Hz：位置更新频率，范围 1–20 Hz。
- Apply speed profile：按已走距离设置分段速度。例如：
    [{"distance_m":0,"speed_ms":2.0},{"distance_m":100,"speed_ms":3.2}]
距离必须递增，速度单位是 m/s；程序按距离平滑过渡。
6.2 启动、暂停、跳转和停止
1. 确认路线至少有两个有效点。
2. 离线测试时保持 Offline preview 勾选。
3. 设置速度、圈数、起点和插值方式。
4. 点击 START。
5. PAUSE 暂停，RESUME 继续，STOP 停止。
6. Jump to point 跳到当前选定点；跳转会重置位置，不计入已走距离。
7. Follow position 将地图视图移到当前模拟位置。
运行时可查看当前经纬度、速度、配速、距离、剩余距离、已用时间、预计剩余时间、路线点/圈数和进度。ETA 是按当前速度估算。Home 显示仪表盘和主要控制按钮；分段速度等设置在 Simulation 页面。
7. 连接 iPhone / iPad
设备能力取决于系统服务、配对、开发者服务和 Apple 开发镜像。Diagnostics 显示 PASS 也不代表每个应用都会使用模拟位置；对新 iOS 版本必须以实际能力检测为准。
7.1 连接前准备
1. 在 Windows 安装 Apple Devices，并确认 Apple Mobile Device USB Driver 已安装。
2. 用可传数据的 USB 线连接 iPhone / iPad。
3. 解锁设备；提示“信任此电脑”时，在手机上确认并输入密码。
4. 如设备提供 Developer Mode，在“设置 → 隐私与安全性 → 开发者模式”按系统提示开启并重启。
5. 保持手机解锁和 USB 连接。
7.2 软件内连接
1. 进入 Devices，点击 Refresh。
2. 选中设备，核对名称、型号、iOS 版本和 UDID。
3. 点击 Connect。
4. 若设备需要隧道，点击 Start tunneld 并按 Windows 提示允许权限。
5. 查看 Developer Mode、tunneld、DVT、LocationSimulation 状态。UNKNOWN 表示当前无法确认，不等于已开启或不需要。
6. 在窗口上方 TARGET 选择目标设备。
7. 回到 Home / Simulation，确认目标设备正确，取消 Offline preview，再点击 START。
若状态异常，先运行 Diagnostics 一键诊断，按页面给出的原因和建议处理。不要因为某个状态未知就反复启动定位。
7.3 停止并恢复 GPS
1. 点击 STOP。
2. 设备保持连接时，在 Devices 或 Manual Control 点击 Restore GPS。
3. 等待恢复后再断开 USB 或退出程序。
4. 若 STOP 后设备断开，重新连接再尝试 Restore GPS。
5. 若恢复失败，查看 Diagnostics 和 Logs，不要假设定位已清除。
强制结束程序或拔线可能使清理步骤无法执行。程序异常重启后不会自动启动之前的设备任务。
8. 手动定位
进入 Manual Control，先确认顶部 TARGET。离线预览只在本机演示；要控制设备须取消预览并确保设备已连接。
- 在 Latitude / Longitude 输入坐标，点 SET LOCATION。
- 点击或拖动地图标记可发送位置。
- Step 可选 0.5、1、2、5、10 米或 Custom 自定义。
- W / ↑ 向北；S / ↓ 向南；A / ← 向西；D / → 向东。
- Save position 保存当前位置；Restore saved 恢复保存位置。
- Restore GPS 尝试清除模拟定位。
快捷键只在 Manual Control 页面生效；当光标在文本或数字输入框时不会移动。路线运行时不要同时手动覆盖位置。
9. 保存场地预设
1. 先设置中心位置和当前路线。
2. 进入 Presets，点击 Save current place 并输入名称。
3. 选中预设可写备注，然后点击 Save notes。
4. Favorite 收藏；Duplicate 复制；Rename 重命名。
5. 搜索可按名称或备注过滤；排序可按 Name 或 Date。
6. Load selected 加载中心、路线和地图显示设置。
7. Import / Export 使用 JSON 文件导入或导出场地；Delete selected 删除选中的预设。
场地包括中心坐标、路线、边界包围矩形、缩放级别、地图类型、创建日期和备注。边界默认由路线范围计算；自定义任意边界多边形需要在导出的 JSON 中编辑。
10. 诊断、日志和设置
10.1 一键诊断
打开 Diagnostics，点击一键诊断。结果分为 PASS、FAIL、UNKNOWN、NOT TESTED。没连接设备时，设备相关项目显示 UNKNOWN 或 NOT TESTED 属正常情况。Export report 保存 JSON 报告；发送前检查是否包含设备标识。
10.2 日志
Logs 页面可筛选 ALL、INFO、WARNING、ERROR、DEBUG，支持 Copy logs 和 Export logs。日志通常位于数据目录的 data/logs/geopilot.log。Settings 的 Copy data directory 可复制实际数据目录路径。分享日志前检查是否含 UDID 或个人路径。
10.3 设置与恢复
Settings 可切换 System / Light / Dark 主题、速度单位，并开启下次启动恢复路线工作区。窗口尺寸、地图位置、最近路线和场地等设置会自动保存。
快捷键：Ctrl+S 保存工作区；Ctrl+Z 撤销；Ctrl+Y 重做。异常退出后程序尽量恢复编辑状态，但不会自动恢复设备定位任务。
11. 常见问题
现象	处理方法
Python Launcher was not found	安装 Python 3.12 x64，并保留 Python Launcher；重新打开项目文件夹，再运行 setup.bat。
lzfse、pylzss 编译失败或提示 Visual C++ 14.0	通常是项目环境用了 Python 3.14 或其他版本。安装 Python 3.12 x64，使用最新版项目包，并运行 setup.bat 重建 .venv。
No module named PySide6	依赖安装未完成。运行 setup.bat 并等待 Setup completed。
setup.bat 下载失败	确认网络可访问 Python 包源，留出磁盘空间，并记录窗口最后的错误行。
地图空白	点击 Retry tiles，检查网络、代理或地图服务；网格和坐标编辑仍可用。
地点搜索失败	检查网络，间隔至少 1 秒后重试；也可直接输入纬度、经度。
Devices 没有手机	检查数据线、USB 接口、Apple Devices 驱动；解锁手机并信任电脑，再点 Refresh。
untrusted / locked	解锁设备并在手机上确认“信任此电脑”，再重新连接。
Developer Mode 为 UNKNOWN	表示能力状态无法确认；查看诊断建议并在设备设置中核对。
tunneld / DVT / LocationSimulation 失败	按诊断建议检查驱动、信任、Developer Mode 和开发镜像；部分设备组合可能不支持。
STOP 后未恢复定位	保持设备连接，点击 Restore GPS，再查看 Diagnostics 和 Logs。
路线偏离实际位置	确认坐标是 WGS84，并核实跑道中心；不要混用 GCJ-02 / BD-09。


12. 支持范围与限制
- Offline preview 可在本机编辑、测量、保存路线并测试运动逻辑。
- 当前交付为源码项目与 Windows 安装/运行脚本，尚未提供经过 Windows 和实体 iPhone 完整验收的 EXE。
- 实际设备控制须在目标 Windows 电脑上验证 Apple 驱动、配对、tunneld、Developer Mode、DVT 和 LocationSimulation。
- 在线地图、地点搜索需要网络服务可达。
- 软件不实现绕过反作弊、传感器验证或完整性检测的功能。
Developed by Hjc · 由 Hjc 开发
