# tomcat出现一闪而过

如果tomcat出现一闪而过的情况，可以打开startup.bat，并在文件最后添加pause，以查看出现了什么问题，然后再根据问题逐一解决。如下来的pause，重新启动即可看到效果



```text
rem Check that target executable exists
if exist "%EXECUTABLE%" goto okExec
echo Cannot find "%EXECUTABLE%"
echo This file is needed to run this program
goto end
:okExec

rem Get remaining unshifted command line arguments and save them in the
set CMD_LINE_ARGS=
:setArgs
if ""%1""=="""" goto doneSetArgs
set CMD_LINE_ARGS=%CMD_LINE_ARGS% %1
shift
goto setArgs
:doneSetArgs

call "%EXECUTABLE%" start %CMD_LINE_ARGS%

:end
pause
```

