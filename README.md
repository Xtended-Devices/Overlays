Xtended Overlays
----------------

• Intelligent Profiles

• High Aspect Ratio

• Smart Charging

• Battery Health

• System Info

• FPS Info

• CPU Info

• AOD

• AOD overlay
--------------
This overlay is required for Custom doze package to work

Example:
-------
    <!-- Whether device supports an alt. ambient display -->
    <bool name="config_alt_ambient_display">true</bool>

    <!-- Whether the always on display mode is available. -->
    <bool name="config_dozeAlwaysOnDisplayAvailable">true</bool>

     <!-- Control whether the always on display mode is enabled by default. This value will be used
         during initialization when the setting is still null. -->
    <bool name="config_dozeAlwaysOnEnabled">false</bool>

• System Info Overlay
----------------------
This overlay is required for the Quick Settings System Info overlay that can display 
Cpu temprature, Battery temprature, Gpu frequency & Gpu utilization

To make this overlay display correct info check kernel specific nodes via adb

	$ adb shell

	#cat /sys/class/thermal/thermal_zone4/temp\

the reading of cpu temp should be in range of 20-70 C

 use the multiplier value to make output value correct

 ex: 38600 -> mean 38.6 C...so in that case we use multiplier 1000

	#cat /sys/class/power_supply/battery/temp

the reading of cpu temp should be in range of 20-70 C

 use the multiplier value to make output value correct

 ex: 386 -> mean 38.6 C...so in that case we use multiplier 10

	#cat /sys/kernel/gpu/gpu_clock

	#cat /sys/kernel/gpu/gpu_busy

Example:
-------
<!-- For Your Device Name -->
    <string name="config_sysCPUTemp">/sys/class/thermal/thermal_zone4/temp</string>
    <string name="config_sysBatteryTemp">/sys/class/power_supply/battery/temp</string>
    <string name="config_sysGPUFreq">/sys/kernel/gpu/gpu_clock</string>
    <string name="config_sysGPULoad">/sys/kernel/gpu/gpu_busy</string>
    <integer name="config_sysCPUTempMultiplier">1000</integer>
    <integer name="config_sysBatteryTempMultiplier">10</integer>

• CPU Info
----------

This overlay is used to show the additional CPU temprature in the CPU Info

Example
------
    <!-- The CPU temperature sensor path, defaults to empty -->
    <string name="config_cpuTempSensor" translatable="false">/sys/class/thermal/thermal_zone4/temp</string>

    <!-- The CPU temperature divider, if needed -->
    <integer name="config_cpuTempDivider" translatable="false">10</integer>


• FPS Info
-----------

This overlay is required to specify the kernel node path

To make sure you are using a working node

	$ adb shell

	#cat /sys/devices/virtual/graphics/fb0/measured_fps

Example
------
    <!-- FPSInfoService Fps file path -->
    <string name="config_fpsInfoSysNode" translatable="false">/sys/devices/virtual/graphics/fb0/measured_fps</string>

• High Aspect Ratio
------------------

This overlay is required to make full screen apps function working properly

Example
------
    <!-- Define that we use a higher screen ratio (18:9) than standard (16:9) -->
    <bool name="config_haveHigherAspectRatioScreen">true</bool>

• Smart Charging
----------------

This overlay is required to make Smart Charging feature functioning.

Example
-------
    <!-- Smart Charing is available -->
    <bool name="config_smartChargingAvailable">true</bool>

    <!-- Smart charge sysfs node and value for suspend/resume charging-->
    <string name="config_SmartChargingSysfsNode" translatable="false">/sys/class/power_supply/battery/input_suspend</string>
    <string name="config_SmartChargingSupspendValue" translatable="false">1</string>
    <string name="config_SmartChargingResumeValue" translatable="false">0</string>

• Intelligent profiles
----------------------

This is completely OPTIONAL feature that hooks different Android modes to spectrum profiles
So this feature depends on spectrum implementation

Android Modes:
-------------

Normal Mode     -> Balanced profile

Gaming mode     -> Gaming/Performance profile

Battery mode    -> Battery profile

Screen off mode -> Battery profile

Note: Profiles are selected with their numbers.

Example
-------

    <!-- Whether or not to use intelligent profiles -->
    <bool name="config_intelligent_performance_profile">true</bool>

    <!-- Initially set all to balanced with persist.spectrum.profile=0
    For example if you want to change performance profile from balanced to performance (in my case performance profile is persist.spectrum.profile=1 )
    then set <string name="config_performance_profile" translatable="false">1</string>, override these config via device tree.
    -->
    <string name="config_balanced_profile" translatable="false">0</string>
    <string name="config_performance_profile" translatable="false">3</string>
    <string name="config_powersave_profile" translatable="false">2</string>
    <string name="config_screen_off_profile" translatable="false">2</string>

• Battery Health overlay
------------------------

This overlay is required to get battery health status in battery page in setting app

You will need to check your available kernel nodes before selecting them
Note that nodes availability depends on kernel version

	$ adb shell

	#cat /sys/class/power_supply/bms/charge_now_raw
	1690500					        <--- Current battery capacity

	#cat /sys/class/power_supply/battery/uevent

    POWER_SUPPLY_NAME=battery
    POWER_SUPPLY_INPUT_SUSPEND=0
    POWER_SUPPLY_BATTERY_CHARGING_ENABLED=1
    POWER_SUPPLY_STATUS=Discharging
    POWER_SUPPLY_HEALTH=Good
    POWER_SUPPLY_PRESENT=1
    POWER_SUPPLY_CHARGE_TYPE=N/A
    POWER_SUPPLY_CAPACITY=76
    POWER_SUPPLY_INPUT_CURRENT_LIMITED=0
    POWER_SUPPLY_VOLTAGE_NOW=4019059
    POWER_SUPPLY_VOLTAGE_MAX=4400000
    POWER_SUPPLY_CURRENT_NOW=-363006
    POWER_SUPPLY_CONSTANT_CHARGE_CURRENT_MAX=2500000
    POWER_SUPPLY_CHARGE_TERM_CURRENT=-199
    POWER_SUPPLY_TEMP=322
    POWER_SUPPLY_TECHNOLOGY=Li-poly
    POWER_SUPPLY_STEP_CHARGING_ENABLED=0
    POWER_SUPPLY_SW_JEITA_ENABLED=1
    POWER_SUPPLY_CHARGE_DONE=0
    POWER_SUPPLY_PARALLEL_DISABLE=0
    POWER_SUPPLY_SET_SHIP_MODE=0
    POWER_SUPPLY_DIE_HEALTH=Hot
    POWER_SUPPLY_RERUN_AICL=0
    POWER_SUPPLY_DP_DM=0
    POWER_SUPPLY_CHARGE_CONTROL_LIMIT_MAX=6
    POWER_SUPPLY_CHARGE_CONTROL_LIMIT=0
    POWER_SUPPLY_CHARGE_COUNTER=1713040
    POWER_SUPPLY_CYCLE_COUNT=365			<--- Cycles count node
    POWER_SUPPLY_RECHARGE_SOC=99
    POWER_SUPPLY_CHARGE_FULL=3984000		<--- Design capacity node
    POWER_SUPPLY_CHARGE_FULL_DESIGN=4000
    POWER_SUPPLY_CHARGING_ENABLED=1

Example
-------

<!-- Battery Health -->
        <string name="config_batDesCap">/sys/class/power_supply/bms/charge_full_design</string>
        <string name="config_batCurCap">/sys/class/power_supply/bms/charge_now_raw</string>
        <string name="config_batChargeCycle">/sys/class/power_supply/bms/cycle_count</string>
