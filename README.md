利用 kinect V2 录制TUM 数据集

* 1、安装 iai_kinect2

> https://github.com/code-iai/iai_kinect2

* 2、进行标定，使深度图和彩色图对齐

> https://github.com/code-iai/iai_kinect2/tree/master/kinect2_calibration

* 3、利用 kinect2_bridge开启相机

> https://github.com/code-iai/iai_kinect2/tree/master/kinect2_bridge

有三种分辨率，可以在代码中进行修改
```
    message_filters::Subscriber<sensor_msgs::Image>rgb_sub(nh, "/kinect2/qhd/image_color", 1);
    message_filters::Subscriber<sensor_msgs::Image>depth_sub(nh,"/kinect2/qhd/image_depth_rect",1);
```

hd: 1920x1080
qhd: 960x540
sd: 512x424

* 4、clone 本代码，修改数据储存路径，图像数量

```
string save_path = "/home/cl/data/";  //根据自己需要修改
...
if(counters == 500) // 假设只保存500幅图像
    {
        frgb.close();
        fdepth.close();
        cout << "保存图片成功。\n\n";
        ros::shutdown();
        return;
    } 
```

* 编译

> catkin_make -DCMAKE_BUILD_TYPE="Release"

* 生成可执行文件 get_image_node 

> sudo updatedb

> locate get_image_node 

* 运行

> ./get_image_node
