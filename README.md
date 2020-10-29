# Information extracted about Windows 10 System settings app

- UWP app under c:\windows\ImmersiveControlPanel\SystemSettings.exe

- References settings from c:\windows\ImmersiveControlPanel\Settings\AllSystemSettings_{253E530E-387D-4BC2-959D-E6F86122E5F2}.xml
  - The format is the same as .settingcontent-ms 
  
```
  <?xml version="1.0" encoding="utf-8"?>
<PCSettings>
  <SearchableContent>
    <Filename>AAA_SystemSettings_Accessibility_Display_DisplayBrightness</Filename>
    <SettingIdentity>
      <PageID>SettingsPageEaseOfAccessDisplay</PageID>
      <SettingID>SystemSettings_Accessibility_Display_DisplayBrightness</SettingID>
      <GroupID>SettingsGroupEaseOfAccessMakeEverythingBrighter</GroupID>
    </SettingIdentity>
    <SettingInformation>
      <Description>@{windows?ms-resource://Windows.UI.SettingsAppThreshold/SearchResources/SystemSettings_Accessibility_Display_DisplayBrightness/Description}</Description>
      <HighKeywords>@{windows?ms-resource://Windows.UI.SettingsAppThreshold/SearchResources/SystemSettings_Accessibility_Display_DisplayBrightness/HighKeywords}</HighKeywords>
    </SettingInformation>
  </SearchableContent>
</PCSettings>
```

- Use __inspector__ from Windows SDK to look at the UWP controls of the app while running - PageID and GroupID points to where the control is found and Description & HighKeywords describe the control

[![inspector-analysis.png](https://i.postimg.cc/662JLGJj/inspector-analysis.png)](https://postimg.cc/qgT5pq7y)

- The HighKeywords & Description are used by the search in Start menu

- The values for the resources can be extracted using shell
  ```MakePri.exe /dump /if C:\Windows\SystemResources\Windows.UI.SettingsAppThreshold\pris\Windows.UI.SettingsAppThreshold.en-US.pri```
  - See the file [here](https://github.com/av-virlan/Win10SystemSettingsInfo/blob/main/resources.pri.xml)
  - For example for display some of the entries are:
    | Description | HighKeywords |
    | --- | --- |
    | Automatically adjust color when lighting changes | adaptive color |
    | Adjust strength of adaptive color | adaptive color settings |
    | Night light | sleep;flux;night light settings;blue light reduction |
    
- Example searching in start for "blue light reduction" starts the Settings app -> navigates to the System section -> goes to Display page

[![start-menu-search.png](https://i.postimg.cc/65pHLkv9/start-menu-search.png)](https://postimg.cc/kDLF7hsZ)
