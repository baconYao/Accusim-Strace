#Strace 、 Accusim 操作方法

##相關連結:
*   [AccuSim: Accurate Simulation of Cache Replacement Algorithms](https://engineering.purdue.edu/~ychu/accusim/)

------

##目錄
*   [環境建置](#1)
    -   [Disksim建置](#disksim)
    -   [Accusim建置](#accusim)
*   [Strace](#2)
*   [Accusim](#3)

------
<a name="1"/></a>
##環境建置
*   使用**32bit**的Ubuntu環境
*   取得Accusim的程式碼及學長的程式碼
    -   自己想辦法要



<a name="disksim"/></a>
###Disksim建置
1.  cd asim/disksim/libddbg
    *   輸入`make`並看到下列畫面後，代表成功
    *   ![Alt](http://i.imgur.com/EawmqFB.png)

2.  將asim/disksim內的 .paths.in檔修改，紅色代表絕對路徑，黃色要填相對應的名稱，如下圖
    *   ![alt](http://i.imgur.com/w83iHYV.png)
    *   之後再將 .paths.in的內容完全複製到.paths
    *   再依序將diskmodel、libparam、src內的.paths.in 和 .paths照做即可
        -   PS.要注意相對應的名稱，路徑則填asim/disksim內的 .paths.in寫好的路徑
        -   ex:此為asim/disksim/libparam/.paths.in內容:(和上圖藍色路徑相同)
        -   ![alt](http://i.imgur.com/5mazStP.png)

3.  cd asim/disksim/libparam
    *   修改util.c的line:240
        -   將`default:`加上`break;`
    *   修改util.c的line:828
        -   將`go to next:`和`next`拿掉
        -   再把if(...)移出第二層迴圈，且把!拿掉，完後後如下圖
        -   ![alt](http://i.imgur.com/PDnlWk2.png)
    *   `sudo apt-get install flex` & `sudo apt-get install bison`
    *   修改disksim/libparam/libparam.lex
        -   line:141  yy_current_buffer改成大寫YY_CURRENT_BUFFER
    *   輸入`make`即可

4.  cd asim/disksim/diskmodel
    *   將asim/disksim/diskmodel/modules內的檔案權限全開
        -   輸入`sudo chmod -f 777 *`
    *   修改asim/disksim/diskmodel內的layout_g1.c
        -   line:212 加上`break;`
    *   將diskmodel/modules內所有.c檔做縮排
        -   將fprintf排好，如下圖
        -   ![alt](http://i.imgur.com/fIk2wKx.png)

5.  cd asim/disksim/src
    *   所有.c檔做縮排，同步驟四的做法
    *   修改src/disksim_disk.c
        -   line:1152、1156 的 static拿掉
        -   line:1162的 static拿掉並且縮排
    *   cd asim/disksim 並且`make`，就可make起來disksim

<a name="accusim"/></a>
###Accusim建置
1.  須先完成Disksim的建置
2.  未完待續


------
<a name="2"/></a>
##Strace



------
##Accusim
<a name="3"/></a>





---
---
[NCHU](http://www.nchu.edu.tw/index1.php),[OSNET Lab](http://osnet.cs.nchu.edu.tw/) 2016/05/06

