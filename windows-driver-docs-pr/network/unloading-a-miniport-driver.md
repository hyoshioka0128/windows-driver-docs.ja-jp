---
title: ミニポート ドライバーのアンロード
description: ミニポート ドライバーのアンロード
ms.assetid: c5199a0f-31c3-42e4-8758-cbe480dff682
keywords:
- ミニポートドライバー WDK ネットワーク、アンロード
- NDIS ミニポートドライバー WDK、アンロード
- ミニポートドライバーのアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b29a9e392c9f0bff50b6a88b2e7d376b1a6847e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843009"
---
# <a name="unloading-a-miniport-driver"></a>ミニポート ドライバーのアンロード





NDIS ミニポートドライバーに関連付けられているドライバーオブジェクトは、[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンを指定します。 ドライバーサービスが削除されたすべてのデバイスの*アンロード*ルーチンがシステムによって呼び出されます。 NDIS には、ミニポートドライバーの*アンロード*ルーチンが用意されています。 NDIS は、 *unload*ルーチンからミニポートドライバーの[*miniportdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)関数を呼び出します。

ミニポートドライバーは、 *Miniportdriverunload*から[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)を呼び出す必要があります。

ミニポートドライバーの*Miniportdriverunload*関数も、ドライバー固有のリソースを解放する必要があります。 *Miniportdriverunload*が返された後、システムはドライバーのアンロード操作を完了します。

*Miniportdriverunload*関数の機能はドライバーに固有です。 一般的な規則として、 *Miniportdriverunload*は、ドライバーの初期化中に実行された操作を元に戻す必要があります。 ドライバーの初期化の詳細については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

 

 





