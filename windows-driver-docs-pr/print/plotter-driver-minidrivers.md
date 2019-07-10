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
ms.openlocfilehash: f02db0c5ac05f93a9ccdc18d921e210a03d31401
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717008"
---
# <a name="plotter-driver-minidrivers"></a>プロッター ドライバー ミニドライバー





マイクロソフトのプロッター ドライバーのモデルに固有のミニドライバーは、デバイスの特性を記述するテキスト ファイルから作成されたベンダーから提供されたバイナリは .pcd ですファイルです。

### <a href="" id="ddk-pcd-files-gg"></a>PCD ファイル

生成します。*pcd*ファイルを作成する必要が最初に、テキスト ファイルを使用して、 [PCD ソース ファイルの形式](pcd-source-file-format.md)します。 実行するとする必要があります plotgpc.exe、これは、Windows Driver Kit (WDK) に含まれています。 このプログラムは、テキスト ファイルをバイナリは .pcd ですファイルに変換されます。 次のコマンド構文を使用します。

**plotgpc**_ソース ファイル パス_.txt*ターゲット ファイル パス*は .pcd です

ソースと宛先の両方のファイルの場合は、ファイル名拡張子は明示的に指定する必要があります。既定値はサポートされていません。

サンプル テキスト ファイルに含まれている plotgpc.exe への入力として使用できる、[プロッターのドライバー ファイルをサンプル](sample-plotter-driver-files.md)します。

 

 




