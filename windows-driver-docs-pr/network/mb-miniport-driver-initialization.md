---
title: MB ミニポート ドライバーの初期化
description: MB ミニポート ドライバーの初期化
ms.assetid: cf332eb4-faea-40e3-b313-512f81718267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dd22980b7485d815bdd30fdba8c9fc7d8161703
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844285"
---
# <a name="mb-miniport-driver-initialization"></a>MB ミニポート ドライバーの初期化


次の図は、インターフェイスが MB インターフェイスとして修飾されているかどうかを判断し、デバイスの機能に関する情報を収集するために実行されるプロセスを表しています。 これらの手順は、MB サービスが開始されたときに列挙された MB インターフェイスごとに実行され、サービスの実行中に新しいインターフェイスが到着するたびに実行されます。 太字のラベルは OID 識別子またはトランザクションフロー制御を表し、通常のテキストのラベルは OID 構造内の重要なフラグを表します。

![インターフェイスが mb インターフェイスとして修飾されているかどうかを確立し、デバイスの機能に関する情報を収集する方法を示す図](images/wwandriverinitproc.png)

MB のミニポートドライバーを初期化するには、次の手順に従います。

1.  MB サービスは、同期 (ブロッキング) [OID\_GEN\_物理\_中程度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium)のクエリ要求を送信して、mb デバイスの種類を識別します。 ミニポートドライバーは、 **NdisPhysicalMediumWirelessWan**に応答して、MB デバイスが WWAN デバイスであることを示します。

2.  MB サービスは、同期 (ブロッキング) [OID\_GEN\_MEDIA\_サポートされている](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-supported)クエリ要求をミニポートドライバーに送信して、mb デバイスで使用されているメディアの種類を特定します。 ミニポートドライバーは、イーサネットエミュレーションを使用することを示すために、 **NdisMedium802\_3**で応答します。

3.  MB サービスは、同期 (ブロッキング) [OID\_WWAN\_DRIVER\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)クエリ要求をミニポートドライバーに送信して、ミニポートドライバーがサポートするドライバーモデルのバージョンを識別します。 ミニポートドライバーは、WWAN\_バージョンで応答します。

4.  MB サービスは、非同期 (非ブロッキング) [OID\_WWAN\_DEVICE\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)クエリ要求をミニポートドライバーに送信して、mb デバイスの機能を特定します。 ミニポートドライバーは、要求を受信したことを示す仮の受信確認で応答し、将来、要求された情報を含む通知を送信します。

5.  ミニポートドライバーは、 [**NDIS\_ステータス\_WWAN\_デバイス\_cap**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)通知を mb サービスに送信します。このサービスは、ミニポートドライバーがサポートしているデバイスの容量を示します。 たとえば、ミニポートドライバーが GSM ベースのデバイスをサポートしている場合は、 [**NDIS\_WWAN\_device\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)構造体の**WwanCellularClass**メンバーの**WwanCellularClassGsm**値を指定する必要があります。 ミニポートドライバーが CDMA ベースのデバイスをサポートしている場合は、 **WwanCellularClassCdma**を指定する必要があります。

 

 





