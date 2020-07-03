---
title: OID_WWAN_SAR_TRANSMISSION_STATUS
description: OID_WWAN_SAR_TRANSMISSION_STATUS は、特定の吸収率 (SAR) の送信状態でのモバイルブロードバンド (MB) モデムからの通知を有効または無効にします。
ms.assetid: 83DFEECD-468A-4A76-B881-DA22FBB3F3A6
ms.date: 08/20/2018
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_SAR_TRANSMISSION_STATUS
ms.localizationpriority: medium
ms.openlocfilehash: 78e9bd0363ad2246c310bcd1812867b7a5adb634
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918108"
---
# <a name="oid_wwan_sar_transmission_status"></a>OID_WWAN_SAR_TRANSMISSION_STATUS

OID_WWAN_SAR_TRANSMISSION_STATUS は、特定の吸収率 (SAR) の送信状態でのモバイルブロードバンド (MB) モデムからの通知を有効または無効にします。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返してから、モデムで SAR 送信状態の通知が有効になっているかどうかを示す[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)構造を含む[NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md)状態通知を送信する必要があります。

設定要求の場合、この OID のペイロードには、SAR 転送状態通知を有効にするか無効にするかを指定する[**NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status)構造が含まれます。

## <a name="remarks"></a>注釈

各クエリまたは設定要求の後、ミニポートドライバーは、転送状態の SAR 通知がモデムで有効になっているかどうかを示す[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)構造を返します。

この OID の使用方法の詳細については、「 [MBIM_CID_MS_TRANSMISSION_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support#mbimcidmstransmissionstatus)」を参照してください。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1703**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)

[**NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status)
