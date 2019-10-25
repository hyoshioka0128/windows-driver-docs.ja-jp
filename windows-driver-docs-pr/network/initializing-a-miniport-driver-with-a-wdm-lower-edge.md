---
title: WDM の下端を含むミニポート ドライバーの初期化
description: WDM の下端を含むミニポート ドライバーの初期化
ms.assetid: 1c5b0ec0-5d63-423d-af21-ffd8990f6160
keywords:
- NDIS-WDM ミニポートドライバー WDK ネットワーク、初期化
- NDIS-WDM ミニポートドライバー WDK ネットワーク、上端
- ミニポートドライバー WDK ネットワーク、初期化
- NDIS ミニポートドライバー WDK、初期化
- 逆シリアル化された NDIS ミニポートドライバーの WDK ネットワーク
- NDIS ミニポートドライバー WDK ネットワーク、ドライバーの初期化の下端
- WDM 低エッジ WDK ネットワーク、ドライバーの初期化
- ミニポートドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66dcdb98ad8d1bdb2ddd42489e29b8d19a3b8bd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824568"
---
# <a name="initializing-a-miniport-driver-with-a-wdm-lower-edge"></a>WDM の下端を含むミニポート ドライバーの初期化





オペレーティングシステムによってミニポートドライバーが読み込まれると、NDIS はミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出して、ミニポートドライバーが管理するミニポートインスタンスを初期化します。 WDM が低いミニポートインスタンスを介して通信するために、ミニポートドライバーは、通信を設定するために特定の情報を取得する必要があります。

このミニポートインスタンスの初期化中に、ミニポートドライバーは[**NdisMGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdeviceproperty)関数を呼び出す必要があります。これは、WDM インターフェイスを介してミニポートインスタンスとの通信を設定するために必要なデバイスオブジェクトを取得するためです。 この呼び出しでは、ミニポートドライバーは、 *Miniportadapterhandle*パラメーターのミニポートインスタンスにハンドルを渡し、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造へのポインターを受け取るバッファーを渡します。 ミニポートドライバーは、次のデバイスオブジェクト ( *NextDeviceObject*パラメーター) に対して取得されたポインターを使用して、irp を作成および送信します。 詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。

WDM の下端があるミニポートドライバーは、逆シリアル化されたミニポートドライバーである必要があります。 逆シリアル化されたミニポートドライバーは、要求をすぐに処理するリソースが不足している場合に、送信要求と受信要求の独自のキューを内部で管理します。ミニポートドライバーが逆シリアル化されていない場合、NDIS はこのキューを管理します。 NDIS-WDM ミニポートドライバーは、NDIS 呼び出しのコンテキストの外部でパケットを送受信するため、逆シリアル化する必要があります。 ミニポートインスタンスの初期化中に、NDIS-WDM ミニポートドライバーは、逆シリアル化された機能を指定する必要があります。 すべての NDIS 6.0 およびそれ以降のミニポートドライバーが逆シリアル化されます。

NDIS-WDM ミニポートドライバーを中間ドライバーにすることはできません (上部にはミニポートドライバーインターフェイスを、下部にはプロトコルドライバーインターフェイスを公開するドライバー)。

 

 





