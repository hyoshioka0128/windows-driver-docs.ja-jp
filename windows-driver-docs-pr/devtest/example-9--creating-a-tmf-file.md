---
title: 例 9 TMF ファイルを作成します。
description: 例 9 TMF ファイルを作成します。
ms.assetid: bf66431b-7937-4a98-96cf-e06d28793401
keywords:
- Tracefmt WDK、TMF ファイル
- TMF ファイル WDK、Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a4a49d75f47d4f1a194952d376f357e2227a0b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557980"
---
# <a name="example-9-creating-a-tmf-file"></a>例 9:TMF ファイルを作成します。


次のコマンドでは、書式設定および Tracedrv.etl、Tracedrv によって生成されるトレース ログにトレース メッセージを表示する Tracefmt よう指示します。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)、ソフトウェア トレースのように設計されたドライバーのサンプルが記載されて、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

コマンドが含まれています、 **-i** Tracefmt Tracedrv の TMF ファイルを作成するように指示するパラメーター。

```
tracefmt d:\tracedrv\tracedrv.etl -i d:\tracedrv\tracedrv.sys -r d:\tracedrv 
-p d:\tracedrv\tmfs -o d:\tracedrv\tracedrv1.txt -v
```

コマンドを使用して、 **-i** Tracedrv、wdk の Tracedrv.sys をイメージ ファイルへの完全修飾パスを示すパラメーターです。

```
-i d:\tracedrv\tracedrv.sys
```

使用して、 **-r** Tracedrv、Tracedrv.pdb PDB シンボル ファイルの完全なバージョンへの完全修飾パスを示すパラメーターです。 このパラメーターは、ファイル名ではなく指定したパスを指定することに注意してください。 Tracefmt 検索で指定されたイメージ ファイルに基づくシンボル ファイルの正しいバージョン **-i**します。

```
-r d:\tracedrv
```

コマンドを使用して、 **-p**で Tracedrv を作成する TMF ファイルを配置する Tracefmt に出力するためのパラメーター、 **d:\\tracedrv\\tmfs**ディレクトリ。

```
-p d:\tracedrv\tmfs
```

コマンドを使用して、 **-o**パラメーターの出力ファイルを配置する Tracefmt に出力するためにトレース メッセージを書式設定、 **d:\\tracedrv\\tracedrv1.txt**ファイル。 このパラメーターは、Tracedrv.txt.sum ファイル名と同じディレクトリにも概要ファイルを配置します。

```
-o d:\tracedrv\tracedrv1.txt
```

**-V**パラメーターは、詳細 (verbose) メッセージを要求します。

このコマンドに応答してで Tracefmt が検索され、d: で Tracedrv.sys の PDB ファイルが見つかった\\tracedrv ディレクトリ。 手順については、PDB ファイルの書式設定するトレース メッセージを抽出し、ステートメントのように、次の出力で太字で TMF ファイルに保存します。 TMF ファイルの名前は、 [GUID をメッセージ](message-guid.md)Tracedrv でトレース プロバイダーの。 Tracefmt もトレース メッセージのコントロール (TMC) ファイルを作成し、同じディレクトリに配置します。

Tracefmt TMF ファイルで作成された後、Tracedrv.etl トレース ログにトレース メッセージの書式設定命令を検索するファイルを読み取ります。 Default.tmf ファイルと検索、TMf ファイル d: で作成されたことを確認して開始\\tracedrv\\tmfs ディレクトリ。

データが書式設定、前に、Tracefmt はトレース ログのデータを表示します。 データが始まり、**ログ ファイルの d:\\tracedrv\\tracedrv.etl**ステートメント。

出力の最後のステートメントでは、Tracefmt が正常に 13 のイベント トレース ログを書式設定し、Tracedrv1.txt と Tracedrv1.txt.sum ファイルを作成したことを示しています。

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

この Tracefmt 実行のプライマリ出力は、Tracedrv.txt、Tracedrv.etl 内のトレース メッセージの書式設定されたバージョンを含むテキスト ファイルです。 次のテキストは、Tracedrv.txt の内容を示しています。

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

 

 





