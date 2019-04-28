---
title: ICC プロファイルをインストールする
description: ICC プロファイルをインストールする
ms.assetid: d9253ee8-c414-46a9-899f-46ae32cee41a
keywords:
- WDK の印刷、ICC プロファイルのインストールの色の管理
- ICC プロファイル WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf3544b17d9316bd207f280513aaa4ded6b15b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366800"
---
# <a name="installing-icc-profiles"></a>ICC プロファイルをインストールする





プリンターの ICC プロファイルをインストールするでファイルを表示、[プリンター INF ファイル](printer-inf-files.md)します。

2 つの ICC プロファイル ファイルをインストールする .inf ファイルの例を次に示します。 プロファイル ファイルが色のディレクトリに書き込まれることに注意してください、[プリンター dirid](printer-dirids.md) 66003 の値。

```cpp
[Version]
Signature="$Windows NT$"
Provider="My Company" 
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer

[My Company]
"My printer model" = MYDRIVER,My_Printer_Model

[MYDRIVER]
DriverFile=DRVR.DRV
DataFile=DRVR.DRV
CopyFiles=@DRVR.DRV,MY_COLOR_PROFILES
DataSection=MYDATA

[MYDATA]
HelpFile=DRVR.HLP
DefaultDataType=EMF

[MY_COLOR_PROFILES]
profile1.icm
profile2.icm

[DestinationDirs]
DefaultDestDir=11
MY_COLOR_PROFILES =66003
```








