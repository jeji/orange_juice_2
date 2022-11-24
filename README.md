# 我的频道 My Channel 
youtube: https://www.youtube.com/channel/UChTFW-Y9eg54AaTY_yama7A \
bilibili：https://b23.tv/pqzW2up

# 版本信息 Release Note
2022/11/12: v0.8_zero2 Remix from [orange juice for orange pi zero](https://github.com/jeji/orange_juice) based on v0.8 \

**[香橙派Zero版本](https://github.com/jeji/orange_juice_2)** \
**[Version for Orange Pi Zero](https://github.com/jeji/orange_juice_2)**

# 信息 Information
- 除**板子尺寸及GPIO配置与orange juice_zero有所区别**外，其他信息例如BOM等都与[orange juice for orange pi zero](https://github.com/jeji/orange_juice)一致
- **(!)请确保你认真[orange juice for orange pi zero](https://github.com/jeji/orange_juice)说明文档**
- gerber文件夹下为嘉立创EDA导出文件，可直接领券下单 

- Except **GPIO config and board size**, Other inform is same as [orange juice for orange pi zero](https://github.com/jeji/orange_juice)
- **(!)Make sure you read [orange juice for orange pi zero](https://github.com/jeji/orange_juice) carefully**
- The zip file under "gerber" folder is exported from EasyEDA, it can be used to place order on JLC directly

# 软件 Software
**(!) 以下配置依赖香橙派已经被正确配置成klipper客户端** \
具体方法请参考 https://www.klipper3d.org/RPi_microcontroller.html \
**(!) Following configuration is assuming that your pi has been config as a klipper client** \
If not, please refer to  https://www.klipper3d.org/RPi_microcontroller.html 

ADXL345配置 \
ADXL345 configuration 

```
[adxl345]
cs_pin: opi:gpio233
spi_bus: spidev1.0

[resonance_tester]
accel_chip: adxl345
probe_points: 60,60,20 #测试点，需要更改为你机器热床中心点，依次为x,y,z
```

MAX31865配置如下，**(!) 你还需要在本节或者其他文件里定义挤出机其他配置** \
MAX31865 config, **(!) you have to define other extruder value seperately** 

```
[extruder]
sensor_type: MAX31865
sensor_pin: opi:gpio1
spi_software_sclk_pin: opi:gpio70
spi_software_mosi_pin: opi:gpio69
spi_software_miso_pin: opi:gpio72
rtd_nominal_r: 100
rtd_reference_r: 430
rtd_num_of_wires: 2
rtd_use_50Hz_filter: True
```

PWM接口配置 \
PWM Port configuration

下为PWM控制的输出插座，对应插槽PWM1 ~ PWM3 \
**(!) 请注意，由于香橙派内核原因，PWM2和PWM3从系统加电启动到klipper正式运行前，默认为高电平，即为打开状态。待klipper正式运行后恢复设置状态** \
PWM control input-voltage output slot \
**(!) Pay attention, because of the linux kernel complied by Orange Pi, the PMW2 and PWM3 is on HIGH (ON) from the power on till klipper start functioning**
```
[fan_generic PWM1_Fan]
pin: opi:gpio74
max_power: 1
shutdown_speed: 0
cycle_time: 0.01
#hardware_pwm:
kick_start_time: 0.5
off_below: 0.1
#enable_pin:
#   See the "fan" section for a description of the above parameters.

[fan_generic PWM2_Fan]
pin: opi:gpio78
max_power: 1
shutdown_speed: 0
cycle_time: 0.01
#hardware_pwm:
kick_start_time: 0.5
off_below: 0.1
#enable_pin:
#   See the "fan" section for a description of the above parameters.

[fan_generic PWM3_Fan]
pin: opi:gpio79
max_power: 1
shutdown_speed: 0
cycle_time: 0.01
#hardware_pwm:
kick_start_time: 0.5
off_below: 0.1
#enable_pin:
#   See the "fan" section for a description of the above parameters.
```
