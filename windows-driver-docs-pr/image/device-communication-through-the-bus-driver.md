---
title: バス ドライバーを使用したデバイス通信
description: バス ドライバーを使用したデバイス通信
ms.assetid: 093e95db-dc3e-467b-9163-e61d793c042e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0670f10de09ebd9d6c9fc13ab0b07163b61cba48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548796"
---
# <a name="device-communication-through-the-bus-driver"></a>バス ドライバーを使用したデバイス通信





WIA ミニドライバーの主な役割では、デバイスと通信します。 その要求を使用して、WIA ミニドライバーのインターフェイスに転送されます WIA アプリケーションが、WIA サービスへの呼び出しを行うと、 [IStiUSD](istiusd-com-interface.md)または[IWiaMiniDrv](https://msdn.microsoft.com/library/windows/hardware/ff545027)インターフェイス。 場合によっては、WIA ミニドライバーに物理デバイスを照会またはデバイス上の他の何らかのアクションを実行する必要があります。 ミニドライバーのデバイスの通信レイヤーは、デバイスが理解できる、要求に WIA サービスからの要求を変換すると、バス ドライバー スタックを介してデバイスに要求を送信します。 同様に、デバイスは、バス ドライバー スタックのバックアップには、その応答を送信するとき、デバイスの通信レイヤーが WIA サービスで認識される応答に、デバイスからの応答を変換する責任を負います。

呼び出しを使用して、バス ドライバー スタックとすべての通信が実行される、 [ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 **ReadFile**、 **WriteFile**、および**DeviceIoControl**関数で、Microsoft Windows SDK のドキュメントに記載されています。 バス ドライバー スタックとの通信の詳細については、次を参照してください。[静止画像デバイスへのアクセスのカーネル モードのドライバー](accessing-kernel-mode-drivers-for-still-image-devices.md)します。

 

 




