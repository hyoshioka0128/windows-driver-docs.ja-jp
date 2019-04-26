---
title: WIA ミニドライバー インターフェイス
description: WIA ミニドライバー インターフェイス
ms.assetid: 6d069584-f9e1-4312-b8f2-1ef3d518faeb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2442972a981387a344df5d1b0d11533d4748b75b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343788"
---
# <a name="wia-minidriver-interfaces"></a>WIA ミニドライバー インターフェイス





WIA ミニドライバーは、標準を実装する COM オブジェクト**IUnknown** (これは、Microsoft Windows SDK ドキュメントで説明されている) COM インターフェイスと WIA 固有の 2 つの追加インターフェイス。[IStiUSD](istiusd-com-interface.md)と[IWiaMiniDrv](https://msdn.microsoft.com/library/windows/hardware/ff545027)します。

### <a name="istiusd-interface"></a>IStiUSD インターフェイス

**IStiUSD**インターフェイスで定義されている*Stiusd.h*、次の操作を実行します。

-   WIA サービス初めて読み込まれるときに、ドライバーを初期化します。

-   WIA サービス、デバイスで非同期のデバイスの通知をサポートするかどうかを報告するには、ドライバーの機能を返します。

-   ロックし、排他的に使用のデバイスのロックを解除します。

### <a name="iwiaminidrv-interface"></a>IWiaMiniDrv インターフェイス

**IWiaMiniDrv**インターフェイスで定義されている*Wiamindr.h*、WIA ミニドライバーの機能のほとんどを公開します。 このインターフェイスは、次の操作を実行します。

-   静止画像デバイスの既定値と現在の設定を定義します。

-   静止画像デバイスのサポートされているコマンドとイベントを定義します。

-   (これは、最終的には、呼び出し元アプリケーションに渡します)、WIA サービスにデバイスからデータを転送します。

これらのインターフェイスの詳細については、次を参照してください。 [WIA ドライバーの開発。基本的な概念](developing-a-wia-driver--basic-concepts.md)します。

 

 




