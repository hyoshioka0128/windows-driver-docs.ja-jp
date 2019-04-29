---
title: プロッター ドライバーのコンポーネント
description: プロッター ドライバーのコンポーネント
ms.assetid: 6a976956-c188-4d31-b176-e97e09e8cc0b
keywords:
- プロッター ドライバー WDK の印刷、コンポーネント
- MSPlot WDK の印刷、コンポーネント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca72ad8a69679f708a65dada9be031724c1de4eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331204"
---
# <a name="plotter-driver-components"></a>プロッター ドライバーのコンポーネント





次の図に示すように、Dll ファイルとバイナリ データ ファイルの MSPlot コンポーネントで構成されます。

![msplot コンポーネントがの dll とバイナリ データ ファイルで構成する方法を示す図](images/msplot.png)

図ではコンポーネントは次のとおりです。

<a href="" id="application"></a>**アプリケーション**  
印刷機能をユーザーに提供するユーザー アプリケーションを指定します。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
ユーザー モード DLL Win32 GDI 関数をエクスポートします。

<a href="" id="kernel-mode-graphics-engine"></a>**カーネル モードのグラフィックス エンジン**  
GDI の機能を実装するオペレーティング システムの NT ベースの executive コード。

<a href="" id="minidrivers"></a>**ミニドライバー**  
MSPlot ミニドライバー (は .pcd ですファイル)。

<a href="" id="cached--pcd-file-data"></a>**ファイル データのキャッシュは .pcd です。**  
ミニドライバーのデータは .pcd ですファイルから読み取る。

<a href="" id="plotui-dll"></a>**plotui.dll**  
[ドライバーのユーザー インターフェイスのプロッター](plotter-driver-user-interface.md) MSPlot でサポートされているすべてのプリンターの共通の UI コードを提供する DLL です。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md)プリンターのユーザー インターフェイス。

<a href="" id="plotter-dll"></a>**plotter.dll**  
[プロッター ドライバー レンダラー](plotter-driver-renderer.md)スプーラーにイメージ データのストリームを送信して画像を表示します。

 

 




