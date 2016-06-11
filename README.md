#Strace 、 Accusim 操作方法

##相關連結:
*   [AccuSim: Accurate Simulation of Cache Replacement Algorithms](https://engineering.purdue.edu/~ychu/accusim/)

------

##目錄
*   [注意事項](#0)
*   [環境建置](#1)
    -   [相關套件](#dependency)
    -   [Disksim建置](#disksim)
        +   [路徑設定](#path)
        +   [Make libddbg](#libddbg)
        +   [Make libparam](#libparam)
        +   [Make DiskModel](#DiskModel)
    -   [Accusim建置](#accusim)
*   [Strace](#2)
*   [Accusim](#3)

------
<a name="0"/></a>
##注意事項
*   此說明文件之內容僅供參考，基於不同的環境和套件版本，可能產生不同的問題

<a name="1"/></a>
##環境建置
*   使用**32bit Linux OS**(例如：Ubuntu 14.04 x86)
*   取得Accusim的程式碼及學長的程式碼
    -   自己想辦法要

<a name="dependency"/></a>
###相關套件
1.   g++
    >   Released by the Free Software Foundation, g++ is a *nix-based C++ compiler usually operated via the command line
    
    安裝指令：`sudo apt-get install g++ build-essential`
2.   bison
    >   Bison is a general-purpose parser generator that converts an annotated context-free grammar into a deterministic LR or generalized LR (GLR) parser employing LALR(1) parser tables
    
    安裝指令：`sudo apt-get install bison`
3.   flex
    >   Flex is a tool for generating scanners. A scanner, sometimes called a tokenizer, is a program which recognizes lexical patterns in text.
    
    安裝指令：`sudo apt-get install flex`

<a name="disksim"/></a>
###Disksim建置

<a name="path"/></a>
#### 路徑設定
1.  將asim/disksim內的 .paths.in檔修改，紅色代表絕對路徑，黃色要填相對應的名稱，如下圖：
    *   ![alt](http://i.imgur.com/w83iHYV.png)
    *   之後再將 .paths.in的內容完全複製到.paths
    *   再依序將diskmodel、libparam、src內的.paths.in 和 .paths照做即可
        -   PS.要注意相對應的名稱，路徑則填asim/disksim內的 .paths.in寫好的路徑
        -   ex:此為asim/disksim/libparam/.paths.in內容:(和上圖藍色路徑相同)
        -   ![alt](http://i.imgur.com/5mazStP.png)

<a name="libddbg"/></a>
#### Make libddbg
1.  `cd asim/disksim/libddbg`
    *   輸入`make`並看到下列畫面後，代表成功
    *   ![Alt](http://i.imgur.com/EawmqFB.png)

<a name="libparam"/></a>
#### Make libparam
>   This is libparam 1.0, a library providing parsing and unparsing of DiskSim/diskmodel parameter files.

1.  `cd asim/disksim/libparam`
    *   修改util.c的line:240
        -   將`default:`加上`break;`
    *   修改util.c的line:828
        -   將`go to next:`和`next`拿掉
        -   再把if(...)移出第二層迴圈，且把!拿掉，完後後如下圖：
        -   ![alt](http://i.imgur.com/PDnlWk2.png)
    *   編譯過程需要[相關套件flex & bison](#dependency)
    *   修改disksim/libparam/libparam.lex
        -   目的在於使用Flex library所定義的常數，推測舊版常數名為yy_current_buffer，造成Compile error
        -   line:141  yy_current_buffer改成大寫YY_CURRENT_BUFFER
    *   輸入`make`即可

<a name="DiskModel"/></a>
#### Make DiskModel
>   This is DiskModel 1.0, a library for modelling disk drive mechanics and layout.

1.  `cd asim/disksim/diskmodel`
    *   將asim/disksim/diskmodel/modules內的檔案權限全開
        -   輸入`sudo chmod -f 777 *`
    *   修改asim/disksim/diskmodel內的layout_g1.c
        -   line:212 加上`break;`
    *   將diskmodel/modules內所有.c檔做縮排
        -   目的在於刪除 \"%s\" 與 " 之間的換行，避免fprintf的參數不完整，而造成Compile error
        -   將fprintf排好，如下圖：
        -   ![alt](http://i.imgur.com/fIk2wKx.png)
    *   在disksim/diskmodel/modules `make`即可

2.  cd asim/disksim/src/modules
    *   所有.c檔做縮排，同前一步驟做法
    *   修改src/disksim_disk.c
        -   line:1152(**disk_get_number_of_blocks**)和1156(**disk_get_numcyls**)的 static刪除
        -   line:1162(**disk_get_mapping**)的 static刪除並且縮排
    *   在disksim/src `make`即可
    *   cd asim/disksim 並且`make`，即可完成Disksim建置

<a name="accusim"/></a>
###Accusim建置
1.  須先完成Disksim的建置
2.  編譯過程需要[相關套件g++](#dependency)
3.  `cd asim/sim` & `make`即可
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

