---
title: WIA ドライバーのコンポーネント
description: WIA ドライバーのコンポーネント
ms.assetid: 2c854945-2eda-4f4c-9cf6-5525e6e237ed
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ffb0d5a7f392a4d02334950292297ea6fa48831
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840710"
---
# <a name="wia-driver-components"></a>WIA ドライバーのコンポーネント





WIA ミニドライバーは、次の2つの論理層として表示できます。

-   WIA サービスインターフェイスレイヤー

-   デバイス通信レイヤー

次の図は、WIA ミニドライバーとそのコンポーネントの論理的な内訳を示しています。

![wia ミニドライバーとそのコンポーネントを示す図](images/art-minidrv.png)

### <a name="wia-minidriver-interfaces"></a>WIA ミニドライバー インターフェイス

WIA ミニドライバーは、 **IUnknown** com インターフェイスを実装する com オブジェクトと、2つの WIA 固有 com インターフェイスである、 [Iz usd](istiusd-com-interface.md)と[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)です。 WIA ミニドライバーインターフェイスレイヤーはこれらのインターフェイスを実装し、WIA ミニドライバーへのエントリポイントです。 アプリケーションは、WIA ミニドライバーインターフェイスを直接呼び出すことはありません。これらのインターフェイスを呼び出すのは、WIA サービスだけです。

### <a name="device-communication"></a>デバイスの通信

デバイス通信レイヤーは、カーネルモードバスドライバーを介して、静止イメージデバイスとの低レベルの対話を行います。 デバイスとのすべてのやり取りは、このレイヤーを介して送信されます。 このレイヤーは、デバイスに送信されるデータを、物理デバイスが認識できる形式にパッケージ化し、デバイスから受信したデータをドライバーが認識する形式に unpackaging する役割を担います。

このセクションでは、次の領域における WIA ミニドライバーとそのコンポーネントに関する追加情報を提供します。

[WIA ミニドライバーインターフェイス](wia-minidriver-interfaces.md)

[バスドライバー経由のデバイス通信](device-communication-through-the-bus-driver.md)

[WIA コンポーネント](wia-components.md)

 

 




