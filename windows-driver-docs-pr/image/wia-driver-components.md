---
title: WIA ドライバーのコンポーネント
description: WIA ドライバーのコンポーネント
ms.assetid: 2c854945-2eda-4f4c-9cf6-5525e6e237ed
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab7460db9c4b59e609d807bdb21600cf53134ea0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383779"
---
# <a name="wia-driver-components"></a>WIA ドライバーのコンポーネント





WIA ミニドライバーは、2 つの論理レイヤーとして表示できます。

-   WIA サービス インターフェイス層

-   デバイスの通信レイヤー

次の図は、WIA ミニドライバーとそのコンポーネントの論理の内訳を示します。

![wia ミニドライバーとそのコンポーネントを示す図](images/art-minidrv.png)

### <a name="wia-minidriver-interfaces"></a>WIA ミニドライバー インターフェイス

WIA ミニドライバーが実装する COM オブジェクト、 **IUnknown** COM インターフェイスと 2 つの WIA 固有の COM インターフェイス。[IStiUSD](istiusd-com-interface.md)と[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)します。 WIA ミニドライバー インターフェイス レイヤーは、これらのインターフェイスを実装し、WIA ミニドライバーへのエントリ ポイントです。 アプリケーションは、WIA ミニドライバー インターフェイスを直接呼び出しません。WIA サービス呼び出しのみにこれらのインターフェイス。

### <a name="device-communication"></a>デバイスの通信

デバイスの通信レイヤーでは、カーネル モードのバス ドライバーを介して静止画像デバイスとの低レベルの対話を担当します。 デバイスとすべてのやり取りは、このレイヤーを介して送信されます。 このレイヤーは、物理デバイスが理解できる形式に、デバイスに送信されるデータをパッケージ化し、ドライバーで認識される形式に、デバイスから受信したアンパッケージ化データ。

このセクションでは、WIA ミニドライバーと、次の領域には、そのコンポーネントについて説明します。

[WIA ミニドライバー インターフェイス](wia-minidriver-interfaces.md)

[バス ドライバーを使用したデバイス通信](device-communication-through-the-bus-driver.md)

[WIA コンポーネント](wia-components.md)

 

 




