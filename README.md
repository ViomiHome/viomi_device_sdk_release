# viomi_device_sdk_release
一、引用sdk版本
（1）修改项目路径下的build.gradle文件

allprojects {
    repositories {
        ...
        maven {
            url 'https://raw.githubusercontent.com/MiEcosystem/mijiaSDK/stable3.0/repository'
        }
        maven {
            url "https://raw.githubusercontent.com/ViomiHome/viomi_device_sdk_release/master"
        }
    }
}
（2）修改app路径下的build.gradle文件
  dependencies {
  implementation 'com.viomi.devicelib:viomi-device-lib:1.4.8' 
}

二、添加代码
（1）在Application oncreate()方法中初始化SDK，
  DeviceCentre.getInstance().init(this, "android");  //初始化sdk,type设备类型（android, ios）,一开始没用用户登录可以默认安卓，后面根据登录用户是android还是ios进行填入。

（2）设置设备回调监听
	
	DeviceCentre.getInstance().addDeviceCallBack(devices -> { //回调设备列表});

（3）A.当用户进行扫码登录时
  /**
     * 登录用户
     *
     * @param accessToken  小米token
     * @param miId         小米id
     * @param macKey       小米macKey
     * @param mExpiresIn   过期时间戳
     * @param macAlgorithm
     * @param type         设备类型
     * @return 是否成功
     */
	
	DeviceCentre.getInstance().loginUser("V3_rHJ218W-tNP0BxP3pq-qgHUUWlyM4QedQPMmZXo9uvoWXTAsyYsHzJHPMtK4KiDw8sR9nFCWUCaYsr8ryIyuxvARmUz3mYDPu_du2ghIEkwpD1AelWuA_MHRVKnjEp_W",
	        "888819681", "UztI53R0UW_lRpvUxl8x1N35F8M", 7776000L, "HmacSHA1", "android");


	String viomiToken = "2J6jdXZEYMsUfgzz"; //云米token
	DeviceCentre.getInstance().refreshRemoteDevices(viomiToken); //搜索设备

   B.下次开启用户已登录，直接调用搜索设备
	DeviceCentre.getInstance().refreshRemoteDevices(viomiToken); //搜索设备
