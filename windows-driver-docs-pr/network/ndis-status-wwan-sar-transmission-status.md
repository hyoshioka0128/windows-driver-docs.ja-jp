---
title: NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS
description: ミニポートドライバーは、NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 通知を使用して、以前の OID_WWAN_SAR_TRANSMISSION_STATUS クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。
ms.assetid: 0F04AC31-A16F-4E6A-A5FF-A69574A300A1
ms.date: 08/20/2018
keywords: -Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS
ms.localizationpriority: medium
ms.openlocfilehash: f9c25655c1a0e676d59c80442720e44ef803ed2e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918014"
---
# <a name="ndis_status_wwan_sar_transmission_status"></a>NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS

ミニポートドライバーは、 **NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS**通知を使用して、以前の[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)クエリまたは設定要求の完了をモバイルブロードバンド (MB) サービスに通知します。

アクティブな無線通信 (OTA) チャネルが変更されると、要請されていないイベントが送信されます。 たとえば、モデムがパケットデータのアップロードを開始した場合、ネットワークデータチャネルを使用してペイロードをアップロードできるようにするには、アップリンクチャネルを設定する必要があります。 これにより、オペレーティングシステムに通知が提供されます。

この通知では、 [**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_TRANSMISSION_STATUS_info)構造を使用します。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1703**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)
