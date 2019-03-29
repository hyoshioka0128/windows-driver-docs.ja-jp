---
title: WIA ドライバーのコンポーネント
description: WIA ドライバーのコンポーネント
ms.assetid: 2c854945-2eda-4f4c-9cf6-5525e6e237ed
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d81e8d335eeaef389dd4d0770e6e96ab908097e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574445"
---
# <a name="wia-driver-components"></a>WIA ドライバーのコンポーネント





WIA ミニドライバーは、2 つの論理レイヤーとして表示できます。

-   WIA サービス インターフェイス層

-   デバイスの通信レイヤー

次の図は、WIA ミニドライバーとそのコンポーネントの論理の内訳を示します。

![wia ミニドライバーとそのコンポーネントを示す図](images/art-minidrv.png)

### <a name="wia-minidriver-interfaces"></a>WIA ミニドライバー インターフェイス

WIA ミニドライバーが実装する COM オブジェクト、 **IUnknown** COM インターフェイスと 2 つの WIA 固有の COM インターフェイス。[IStiUSD](istiusd-com-interface.md)と[IWiaMiniDrv](https://msdn.microsoft.com/library/windows/hardware/ff545027)します。 WIA ミニドライバー インターフェイス レイヤーは、これらのインターフェイスを実装し、WIA ミニドライバーへのエントリ ポイントです。 アプリケーションは、WIA ミニドライバー インターフェイスを直接呼び出しません。WIA サービス呼び出しのみにこれらのインターフェイス。

### <a name="device-communication"></a>デバイスの通信

デバイスの通信レイヤーでは、カーネル モードのバス ドライバーを介して静止画像デバイスとの低レベルの対話を担当します。 デバイスとすべてのやり取りは、このレイヤーを介して送信されます。 このレイヤーは、物理デバイスが理解できる形式に、デバイスに送信されるデータをパッケージ化し、ドライバーで認識される形式に、デバイスから受信したアンパッケージ化データ。

このセクションでは、WIA ミニドライバーと、次の領域には、そのコンポーネントについて説明します。

[WIA ミニドライバー インターフェイス](wia-minidriver-interfaces.md)

[バス ドライバーを使用したデバイス通信](device-communication-through-the-bus-driver.md)

[WIA コンポーネント](wia-components.md)

 

 




