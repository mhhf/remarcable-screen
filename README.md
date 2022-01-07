
```sh
%% xrandr --newmode 1408x1872 0 1408 1408 1408 1408 1872 1872 1872 1872
xrandr --newmode 1872x1408 0 1872 1872 1872 1872 1408 1408 1408 1408
%% xrandr --addmode VIRTUAL1 1872x1408
xrandr --addmode VIRTUAL2 1872x1408
xrandr --output VIRTUAL1 --mode 1408x1872 --right-of eDP1
%% xrandr --output VIRTUAL2 --mode 1872x1408 --left-of eDP1
x11vnc -repeat -forever -nocursor -rotate xy -allow 10.11.99.1 -nopw -clip $(xrandr | perl -n -e'/VIRTUAL1.*?(\d+x\d+\+\d+\+\d+)/ && print $1') &
ssh root@10.11.99.1 "systemctl stop xochitl && ./vnsee; systemctl start xochitl"
```
