---
title: MB ミニポート ドライバーの初期化
description: MB ミニポート ドライバーの初期化
ms.assetid: cf332eb4-faea-40e3-b313-512f81718267
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 948eb025627d16e75b0014205a0edd773d16240e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357819"
---
# <a name="mb-miniport-driver-initialization"></a>MB ミニポート ドライバーの初期化


次の図は、MB インターフェイスとしてインターフェイスを修飾するかどうかを判断すると、デバイスの機能に関する情報を収集するプロセスを表します。 次の手順は、サービスの起動時、MB も新しい各インターフェイスが届くと、サービスの実行中に列挙された各 MB インターフェイスに対して実行されます。 太字表す OID の識別子またはトランザクションのフロー制御には、ラベルと通常のテキストに表示されるラベルは、OID 構造内で重要なフラグを表します。

![インターフェイスは mb インターフェイスとして修飾されているかどうかを確立して、デバイスの機能に関する情報を収集するかを示すを示す図](images/wwandriverinitproc.png)

MB のミニポート ドライバーを初期化するには、次の手順を使用します。

1.  MB サービスは、同期 (ブロック) を送信[OID\_GEN\_物理\_MEDIUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium) MB デバイスの種類を識別するためにクエリ要求。 ミニポート ドライバーで応答した**NdisPhysicalMediumWirelessWan** MB デバイスが WWAN デバイスであることを示します。

2.  MB サービスは、同期 (ブロック) を送信[OID\_GEN\_メディア\_サポートされている](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-supported)MB デバイスでの使用のメディアの種類を識別するために、ミニポート ドライバーにクエリ要求。 ミニポート ドライバーで応答した**NdisMedium802\_3**をイーサネット エミュレーションを使用しているかを示します。

3.  MB サービスは、同期 (ブロック) を送信[OID\_WWAN\_ドライバー\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)クエリ要求にどのようなドライバー モデルのバージョンを識別するために、ミニポート ドライバー、ミニポート ドライバーをサポートしています。 ミニポート ドライバーで応答した WWAN\_バージョン。

4.  MB サービスは、非同期 (非ブロッキング) を送信[OID\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps) MB デバイスの機能を識別するために、ミニポート ドライバーにクエリ要求。 ミニポート ドライバーは、要求を受信したことに必要な情報、今後の通知は送信 provisional 受信確認応答します。

5.  ミニポート ドライバーの送信、 [ **NDIS\_状態\_WWAN\_デバイス\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)の機能を示す MB サービスへの通知MB デバイス ミニポート ドライバーをサポートします。 たとえば、ミニポート ドライバーでは、GSM ベースのデバイスをサポートする場合は指定する必要が、 **WwanCellularClassGsm**値、 **DeviceCaps.WwanCellularClass**のメンバー、 [ **NDIS\_WWAN\_デバイス\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)構造体。 これを指定する必要があるかどうか、ミニポート ドライバーは、CDMA ベースのデバイスをサポートする**WwanCellularClassCdma**します。

 

 





