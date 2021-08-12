# Microsoft Windows

## Remove windows.old folder
```
# Remembe to run cmd as administrator
takeown /f %systemdrive%\windows.old /r /d y &&^
forfiles /P %systemdrive%\windows.old /S /C "cmd /c icacls @path /grant Administrators:F" &&^ 
rd /s /q %systemdrive%\windows.old

```

## List files, folders: Fullname, size
```powershell
$pathSource = "Full path of source folder"
$pathDestination = "Full path of destination folder"
$pathLog = "Full path to save result"
gci -Recurse -Path $pathSource | Select-Object FullName, Length | Export-Csv -Path $pathLog\source.csv -NoTypeInformation
gci -Recurse -Path $pathDestination | Select-Object FullName, Length | Export-Csv -Path $pathLog\destination.csv --NoTypeInformation
```

## openSUSE Leap
```powershell
$WSLName = "openSUSE-Leap-15.2"
$Distribution = "*openSUSELeap15.2*"
$WSLRoot = "E:\wsl"
$WSLDir = "opensuseleap15"

New-Item -Type Directory "$WSLRoot\$WSLDir"

Get-AppxPackage $Distribution

wsl --shutdown $WSLName

wsl --export $WSLName "${WSLRoot}\${WSLName}.tar.gz"

if ($? -eq 'True') { Remove-AppxPackage -Package (Get-AppxPackage $Distribution).PackageFullname }

$CheckDistribution = Get-AppxPackage $Distribution

if ($CheckDistribution -eq $null) {wsl --import $WSLName "$WSLRoot\$WSLDir" "${WSLRoot}\${WSLName}.tar.gz"}
```
