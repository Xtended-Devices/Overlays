## Xtended Overlays & flags. 
:point_down: **These Flags should be added into device make file:** :point_down:

```  
# Official Xtended
XTENDED_BUILD_TYPE := OFFICIAL
XTENDED_BUILD_MAINTAINER := yourname
```

```
# Gapps
WITH_GAPPS := true
TARGET_INCLUDE_NGA := true
```

```
# UDFPS Animation
EXTRA_UDFPS_ANIMATIONS := true
```

```
# SOC
PROCESSOR_MODEL := SM8350  

*Change as per your device processor model.
```

```
# Blur
TARGET_ENABLE_BLUR := true
```
#
:point_right: **Add into** *overlay/frameworks/base/core/res/res/values/config.xml*

```
<!-- Whether device has notification LED -->
<bool name="config_hasNotificationLed">true</bool>

<!-- Whether devices suports in-display fingerprint when screen is off -->
<bool name="config_supportScreenOffUdfps">true</bool>
```

:point_right: **If your device has variable screen resolution**
```
<!-- Enforce DisplayModeDirector to select user preferred resolution -->
<bool name="config_forceToUseSelectedResolution">true</bool>
```
:point_right: **If your device has variable refresh rate**
```
<!-- The default peak refresh rate for a given device.  -->
<integer name="config_defaultPeakRefreshRate">120</integer>

*Change 120 to max refresh rate of your device.
```


:point_right: **If your device has LinearmotorVibrator**
```
<!-- Mock Oplus LinearmotorVibratorService -->
<bool name="config_mockOplusLinearmotorVibratorService">true</bool>
```    
#
:point_right: **Add into** *overlay/frameworks/base/packages/SystemUI/res/values/config.xml*

```    
<!-- Whether the combined qs shows in status bar -->
<bool name="flag_combined_qs_headers">false</bool>

<!-- StatusBar burn-in protection -->
<bool name="config_disableStatusBarBurnInProtection">true</bool>

<!-- Max visible notification icons -->
<integer name="config_maxVisibleNotificationIcons">4</integer>
<integer name="config_maxVisibleNotificationIconsOnLock">3</integer>
```

#
:point_right: **Add into** *overlay/packages/apps/Settings/res/values/config.xml*

```
<!-- Whether to show refresh rate in display settings -->
<bool name="config_show_refresh_rate_controls">true</bool>
```
