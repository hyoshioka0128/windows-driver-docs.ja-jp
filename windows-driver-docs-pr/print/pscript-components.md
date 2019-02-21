---
title: Pscript コンポーネント
description: Pscript コンポーネント
ms.assetid: 9f3bd004-e62c-42b6-99da-045c12e088a3
keywords:
- PostScript プリンター ドライバー WDK の印刷、コンポーネント
- Pscript WDK の印刷、コンポーネント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93d4b7640cb477f254c967766dff0fe8251f255f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558418"
---
# <a name="pscript-components"></a>Pscript コンポーネント





次の図に示すように、Dll、およびテキストおよびバイナリ データのファイルの Pscript コンポーネントで構成されます。

![pscript コンポーネントを示す図は、dll、およびテキストおよびバイナリ データ ファイルで構成されています](images/pscript5.png)

図ではコンポーネントは次のとおりです。

<a href="" id="application"></a>**アプリケーション**  
印刷機能を持つユーザーを提供する、ワード プロセッサなどのユーザー アプリケーション。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
ユーザー モード DLL Win32 GDI 関数をエクスポートします。

<a href="" id="kernel-mode-graphics-engine"></a>**カーネル モードのグラフィックス エンジン**  
GDI の機能を実装するオペレーティング システムの NT ベースの executive コード。

<a href="" id="minidriver-text-files"></a>**ミニドライバーのテキスト ファイル**  
テキスト ベースの Pscript ミニドライバー ファイル。

<a href="" id="binary-data-files"></a>**バイナリ データ ファイル**  
一時ファイル (拡張子を .bpd) Pscript をミニドライバー テキスト ファイルに含まれる情報を解析後に作成します。

<a href="" id="ps5ui-dll"></a>**ps5ui.dll**  
[ユーザー インターフェイスの Pscript](pscript-user-interface.md) Pscript でサポートされているすべてのプリンターの共通の UI コードを提供する DLL です。

<a href="" id="user-interface-plug-in"></a>**プラグインのユーザー インターフェイス**  
省略可能なプリンター固有[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)します。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md)プリンターのユーザー インターフェイス。

<a href="" id="pscript5-dll"></a>**pscript5.dll**  
[Pscript レンダラー](pscript-renderer.md)、画像を表示し、印刷スプーラーにテキストとイメージ データを送信するテキスト出力を処理します。

<a href="" id="rendering-plug-in"></a>**プラグインの表示**  
省略可能なプリンター固有[プラグインでレンダリング](rendering-plug-ins.md)します。

 

 




