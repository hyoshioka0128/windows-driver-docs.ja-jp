---
title: Unidrv コンポーネント
description: Unidrv コンポーネント
ms.assetid: 358eed9e-05e3-4670-b6b1-d5413c46edf0
keywords:
- Unidrv、コンポーネント
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c6f418e7853cf03eadb19feb0fb07438128c872
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558634"
---
# <a name="unidrv-components"></a>Unidrv コンポーネント





次の図に示すように、Dll、およびテキストおよびバイナリ データのファイルの Unidrv コンポーネントで構成されます。

![dll の場合、追加テキストおよびバイナリ データ ファイルの unidrv コンポーネントの構成方法を示す図](images/unidrvcm.png)

図ではコンポーネントは次のとおりです。

<a href="" id="application"></a>**アプリケーション**  
印刷機能を持つユーザーを提供する、ワード プロセッサなどのユーザー アプリケーション。

<a href="" id="gdi32-dll"></a>**gdi32.dll**  
ユーザー モード DLL Win32 GDI 関数をエクスポートします。

<a href="" id="kernel-mode-graphics-engine-------"></a>カーネル モードのグラフィックス エンジン   
GDI の機能を実装して NT executive コード。

<a href="" id="minidriver-text-files"></a>**ミニドライバーのテキスト ファイル**  
テキスト ベース[Unidrv ミニドライバー](unidrv-minidrivers.md)を使用してプリンターを記述する[GPD ファイル エントリ](gpd-file-entries.md)します。

<a href="" id="binary-data-files"></a>**バイナリ データ ファイル**  
一時ファイル (拡張子を .bud) Unidrv をミニドライバー テキスト ファイルに含まれる情報を解析後に作成します。

<a href="" id="unidrvui-dll"></a>**unidrvui.dll**  
[ユーザー インターフェイスの Unidrv](unidrv-user-interface.md) Unidrv でサポートされているすべてのプリンターの共通の UI コードを提供する DLL です。

<a href="" id="user-interface-plug-in"></a>**プラグインのユーザー インターフェイス**  
省略可能なプリンター固有[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)します。

<a href="" id="compstui-dll"></a>**compstui.dll**  
[CPSUI](common-property-sheet-user-interface.md)プリンターのユーザー インターフェイス。

<a href="" id="unidrv-dll"></a>**unidrv.dll**  
[Unidrv レンダラー](unidrv-renderer.md)画像を表示し、印刷スプーラーをイメージのデータ ストリームを送信します。

<a href="" id="rendering-plug-in"></a>**プラグインの表示**  
省略可能なプリンター固有[プラグインでレンダリング](rendering-plug-ins.md)します。

 

 




