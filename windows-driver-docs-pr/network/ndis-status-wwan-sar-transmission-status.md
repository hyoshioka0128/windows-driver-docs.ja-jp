---
title: NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 通知を使用して、以前の OID_WWAN_SAR_TRANSMISSION_STATUS クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 0F04AC31-A16F-4E6A-A5FF-A69574A300A1
ms.date: 08/20/2018
keywords: -Windows Vista 以降の NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 56799aa77088fee7be66d1efe8d4884c089b3ae1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844645"
---
# <a name="ndis_status_wwan_sar_transmission_status"></a>NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS

ミニポートドライバーは、 **NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS**通知を使用して、以前の[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

アクティブな無線通信 (OTA) チャネルが変更されると、要請されていないイベントが送信されます。 たとえば、モデムがパケットデータのアップロードを開始した場合、ネットワークデータチャネルを使用してペイロードをアップロードできるようにするには、アップリンクチャネルを設定する必要があります。 これにより、オペレーティングシステムに通知が提供されます。

この通知では、 [**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_TRANSMISSION_STATUS_info)構造体が使用されます。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)
