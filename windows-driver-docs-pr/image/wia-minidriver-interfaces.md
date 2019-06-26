---
title: WIA ミニドライバー インターフェイス
description: WIA ミニドライバー インターフェイス
ms.assetid: 6d069584-f9e1-4312-b8f2-1ef3d518faeb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ee0ffb88e52755355ab565fbbcef502342e0a44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355185"
---
# <a name="wia-minidriver-interfaces"></a>WIA ミニドライバー インターフェイス





WIA ミニドライバーは、標準を実装する COM オブジェクト**IUnknown** (これは、Microsoft Windows SDK ドキュメントで説明されている) COM インターフェイスと WIA 固有の 2 つの追加インターフェイス。[IStiUSD](istiusd-com-interface.md)と[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)します。

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

 

 




