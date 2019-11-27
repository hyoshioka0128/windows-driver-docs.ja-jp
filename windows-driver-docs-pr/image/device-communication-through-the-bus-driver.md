---
title: バス ドライバーを使用したデバイス通信
description: バス ドライバーを使用したデバイス通信
ms.assetid: 093e95db-dc3e-467b-9163-e61d793c042e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 909f8ab2875e2c70557214b3ce8cf3f3d03bd0aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840857"
---
# <a name="device-communication-through-the-bus-driver"></a>バス ドライバーを使用したデバイス通信





WIA ミニドライバーの主な役割は、デバイスと通信することです。 Wia アプリケーションが WIA サービスを呼び出すと、その要求は[iIWiaMiniDrv](istiusd-com-interface.md)インターフェイスまたは[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)インターフェイスを介して、wia ミニドライバーのインターフェイスに転送されます。 場合によっては、WIA ミニドライバーが物理デバイスに対してクエリを実行するか、デバイスで他のアクションを実行する必要があります。 ミニドライバーのデバイス通信レイヤーは、WIA サービスからの要求を、デバイスが認識できる要求に変換し、バスドライバースタックを介してデバイスに要求を送信する役割を担います。 同様に、デバイスが応答をバスドライバースタックに送信すると、デバイス通信レイヤーは、デバイスからの応答を、WIA サービスが認識できる応答に変換する役割を担います。

バスドライバースタックとの通信はすべて、Microsoft Windows SDK のドキュメントで説明されている[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**、および**DeviceIoControl**の各関数の呼び出しを使用して実行されます。 バスドライバースタックとの通信の詳細については、「[イメージデバイス用のカーネルモードドライバーへのアクセス](accessing-kernel-mode-drivers-for-still-image-devices.md)」を参照してください。

 

 




