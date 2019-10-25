---
title: OID_WWAN_SAR_TRANSMISSION_STATUS
description: OID_WWAN_SAR_TRANSMISSION_STATUS は、特定の吸収率 (SAR) の送信状態でのモバイルブロードバンド (MB) モデムからの通知を有効または無効にします。
ms.assetid: 83DFEECD-468A-4A76-B881-DA22FBB3F3A6
ms.date: 08/20/2018
keywords: -Windows Vista 以降の OID_WWAN_SAR_TRANSMISSION_STATUS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 7374ca461a7ca81de4e2cae12522fb61249b1f43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843796"
---
# <a name="oid_wwan_sar_transmission_status"></a>OID_WWAN_SAR_TRANSMISSION_STATUS

OID_WWAN_SAR_TRANSMISSION_STATUS は、特定の吸収率 (SAR) の送信状態でのモバイルブロードバンド (MB) モデムからの通知を有効または無効にします。

ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に NDIS_STATUS_INDICATION_REQUIRED を元の要求に戻してから、 [NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md)ステータス通知をSAR 送信状態の通知がモデムで有効になっているかどうかを示す[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)構造体。

設定要求の場合、この OID のペイロードには、SAR 転送状態通知を有効にするか無効にするかを指定する[**NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status)構造体が含まれます。

## <a name="remarks"></a>注釈

各クエリまたは設定要求の後、ミニポートドライバーは、転送状態の SAR 通知がモデムで有効になっているかどうかを示す[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)構造体を返します。

この OID の使用方法の詳細については、「 [MBIM_CID_MS_TRANSMISSION_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support#mbimcidmstransmissionstatus)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1703 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)

[**NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status)
