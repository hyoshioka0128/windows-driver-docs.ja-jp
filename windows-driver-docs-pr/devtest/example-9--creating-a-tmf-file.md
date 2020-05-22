---
title: 例 9 TMF ファイルを作成する
description: 例 9 TMF ファイルを作成する
ms.assetid: bf66431b-7937-4a98-96cf-e06d28793401
keywords:
- Tracefmt WDK、TMF ファイル
- TMF ファイル WDK、Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e6acce66011268d3bd0ddac50ff16014cd0db2f
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769672"
---
# <a name="example-9-creating-a-tmf-file"></a>例 9: TMF ファイルを作成する


次のコマンドは、Tracefmt に対して、tracefmt によって生成されるトレースログである Tracefmt のトレースメッセージを書式設定して表示するように指示します。 ソフトウェアトレース用に設計された[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)は、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

コマンドには、 **-i**パラメーターが含まれています。これにより、Tracefmt は Tracefmt の tmf ファイルを作成するように指示します。

```
tracefmt d:\tracedrv\tracedrv.etl -i d:\tracedrv\tracedrv.sys -r d:\tracedrv 
-p d:\tracedrv\tmfs -o d:\tracedrv\tracedrv1.txt -v
```

このコマンドは、 **-i**パラメーターを使用して、WDK の tracedrv のイメージファイルへの完全修飾パスを指定します。

```
-i d:\tracedrv\tracedrv.sys
```

この例では、 **-r**パラメーターを使用して、Tracedrv の pdb シンボルファイルの完全修飾パスを示しています。 このパラメーターを使用してパスを指定することに注意してください。ただし、ファイル名は指定しないでください。 Tracefmt は、 **-i**によって指定されたイメージファイルに基づいて、正しいバージョンのシンボルファイルを検索します。

```
-r d:\tracedrv
```

このコマンドは、 **-p**パラメーターを使用して Tracefmt に対して、tracefmt 用に作成された tmf ファイルを**d: \\ tracefmt \\ tmfs**ディレクトリに配置するように指示します。

```
-p d:\tracedrv\tmfs
```

このコマンドは、 **-o**パラメーターを使用して、トレースメッセージの出力ファイルを**d: \\ tracefmt \\ tracedrv1**ファイルに配置するように tracefmt に指示します。 また、このパラメーターを指定すると、同じディレクトリ内に Tracedrv ファイル名で概要ファイルが配置されます。

```
-o d:\tracedrv\tracedrv1.txt
```

**-V**パラメーターは詳細な (詳細) メッセージを要求します。

このコマンドに応答して、Tracefmt は d: \\ tracefmt ディレクトリで Tracefmt の PDB ファイルを検索して検索します。 次の出力の太字で示されているように、PDB ファイルからトレースメッセージの書式設定命令を抽出し、TMF ファイルに格納します。 TMF ファイルの名前は、Tracedrv のトレースプロバイダーの[メッセージ GUID](message-guid.md)です。 また、tracefmt はトレースメッセージ制御 (TMC) ファイルを作成し、同じディレクトリに配置します。

Tracefmt によって TMF ファイルが作成された後、ファイルが読み取られ、Tracefmt トレースログ内のトレースメッセージの書式設定手順が検索されます。 最初に、既定の tmf ファイルから、d: \\ tracedrv tmfs ディレクトリに作成された TMf ファイルを検索します。 \\

データを書式設定する前に、Tracefmt はトレースログに関するデータを表示します。 データは、 **Logfile d: \\ tracedrv \\ tracステートメント**で始まります。

出力の最後のステートメントは、Tracefmt がトレースログで13個のイベントを正常にフォーマットし、Tracedrv1 ファイルと Tracedrv1 ファイルを作成したことを示しています。

```
Setting log file to: d:\tracedrv\tracedrv.etl

Searching for matching PDB to d:\tracedrv\tracedrv.sys
Current Symbol Search Path = d:\tracedrv

Extracting TMF files out of found PDB files
DBGHELP: d:\tracedrv\tracedrv.pdb - OK
tracefmt : info BNP0000: WPPFMT generating d:\tracedrv\tmfs\1606d1a7-1682-57d1-65f7-36693800e096.tmf for d:\tracedrv\tracedrv.pdb
tracefmt : info BNP0000: WPPFMT generating d:\tracedrv\tmfs\d58c126f-b309-11d1-969e-0000f875a5bc.tmc for d:\tracedrv\tracedrv.pdb
Examining C:\WinDDK\5066\tools\tracing\i386\default.tmf for message formats,  3 found.
Searching for TMF files on path: d:\tracedrv\tmfs
Logfile d:\tracedrv\tracedrv.etl:
        OS version              5.1.2600  (Currently running on 5.1.2600)
        Start Time              2005-06-10-14:25:30.827
        End Time                2005-06-10-14:26:14.371
        Timezone is             Pacific Standard Time (Bias is 480mins)
        BufferSize              8192 B
        Maximum File Size       0 MB
        Buffers  Written        2
        Logger Mode Settings    (0) Logfile Mode is not set
        ProcessorCount          1
06/10/2005-21:25:45.539 ::        1: Filled=     696, Lost=  0 TotalLost= 0

Processing completed   Buffers: 1, Events: 13, EventsLost: 0 :: Format Errors: 0, Unknowns: 0

Event traces dumped to d:\tracedrv\tracedrv1.txt
Event Summary dumped to d:\tracedrv\tracedrv1.txt.sum
```

この Tracefmt 実行の主な出力は Tracefmt .txt です。これは、Tracefmt のトレースメッセージの書式設定されたバージョンを含むテキストファイルです。 次のテキストは Tracedrv の内容を示しています。

```
EventTrace
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]IOCTL = 1
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 1 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 2 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 3 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Machine State :: Offline
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]IOCTL = 2
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 1 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 2 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 3 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Machine State :: Offline
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
```

 

 





