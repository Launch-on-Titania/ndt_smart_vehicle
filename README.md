# ndt_smart_vehicle

## Localization in a pointcloud map(pcd)

## How to use

### Prepare pcd map and rosbag
 本次用的bag是 mapping_lidar.bag

把pcd文件放到map文件夹

```
map_v1.pcd 
```

### Build in your ros workspace
把整个仓库文件clone进自己的workspace

### Config map loader
把地图map_v1.pcd放到对应的

```xml
<arg name="pcd_path"  default="$(find ndt_localizer)/map/kaist02.pcd"/>
```
### Config point cloud downsample（我已经配置好）

如果Lidar数据稀疏(如VLP-16)，要配置更小`leaf_size` in `launch/points_downsample.launch` 用 `2.0`. 

如果Lidar点云很密集(VLP-32, Hesai Pander40P, HDL-64等)
 `leaf_size` 用 `3.0`。


### Run the package
上述工作完成后
```bash
roscore

cd catkin_ws

source devel/setup.bash

rosparam set use_sim_time true
```
如果单纯跑 `ndt_localizer` 包， 则运行：
```
roslaunch ndt_localizer ndt_localizer.launch
```
如果同时跑`scan context` 和 `ndt_localizer`则运行：
```
roslaunch ndt_localizer sc_ndt_localizer.launch
```

