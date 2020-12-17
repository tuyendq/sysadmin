# Microsoft Windows

## Remove windows.old folder
```
# Remembe to run cmd as administrator
takeown /f %systemdrive%\windows.old /r /d y &&^
forfiles /P %systemdrive%\windows.old /S /C "cmd /c icacls @path /grant Administrators:F" &&^ 
rd /s /q %systemdrive%\windows.old

```
