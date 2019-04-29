---
title: プロッター ドライバー ミニドライバー
description: プロッター ドライバー ミニドライバー
ms.assetid: f7223a0a-df02-4a4f-a3d6-7910aed926eb
keywords:
- プロッター ドライバー WDK の印刷、ミニドライバー
- MSPlot WDK の印刷、ミニドライバー
- ミニドライバー WDK MSPlot
- PCD ファイル WDK MSPlot
- .pcd ですファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c38dbc5d532a603fc524c6ca7b8313c3813c88f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388071"
---
# <a name="plotter-driver-minidrivers"></a>プロッター ドライバー ミニドライバー





マイクロソフトのプロッター ドライバーのモデルに固有のミニドライバーは、デバイスの特性を記述するテキスト ファイルから作成されたベンダーから提供されたバイナリは .pcd ですファイルです。

### <a href="" id="ddk-pcd-files-gg"></a>PCD ファイル

生成します。*pcd*ファイルを作成する必要が最初に、テキスト ファイルを使用して、 [PCD ソース ファイルの形式](pcd-source-file-format.md)します。 実行するとする必要があります plotgpc.exe、これは、Windows Driver Kit (WDK) に含まれています。 このプログラムは、テキスト ファイルをバイナリは .pcd ですファイルに変換されます。 次のコマンド構文を使用します。

**plotgpc***source-file-path* .txt *target-file-path* .pcd

ソースと宛先の両方のファイルの場合は、ファイル名拡張子は明示的に指定する必要があります。既定値はサポートされていません。

サンプル テキスト ファイルに含まれている plotgpc.exe への入力として使用できる、[プロッターのドライバー ファイルをサンプル](sample-plotter-driver-files.md)します。

 

 




