---
title: OID_WWAN_SAR_TRANSMISSION_STATUS
description: OID_WWAN_SAR_TRANSMISSION_STATUS を有効または特定吸収レート (SAR) 転送状態のモバイル ブロード バンド (MB) モデムからの通知を無効にします。
ms.assetid: 83DFEECD-468A-4A76-B881-DA22FBB3F3A6
ms.date: 08/20/2018
keywords: -OID_WWAN_SAR_TRANSMISSION_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d286f4955b0cd93aca25eb52c21771128a7a7c7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368486"
---
# <a name="oidwwansartransmissionstatus"></a>OID_WWAN_SAR_TRANSMISSION_STATUS

OID_WWAN_SAR_TRANSMISSION_STATUS を有効または特定吸収レート (SAR) 転送状態のモバイル ブロード バンド (MB) モデムからの通知を無効にします。

ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md)状態通知を含む、 [ **NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)行政区の通知転送状態であるかどうかを記述する構造体は、モデムで有効にします。

この OID のペイロードを含む、一連の要求について、 [ **NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status) SAR 転送状態の通知を有効または無効になっているかどうかを指定する構造体。

## <a name="remarks"></a>注釈

各クエリまたは一連の要求後に、ミニポート ドライバーを返す必要があります、 [ **NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)内で行政区の通知転送状態であるかどうかを記述する構造体が有効になっています。モデム。

この OID の使用状況に関する詳細については、次を参照してください。 [MBIM_CID_MS_TRANSMISSION_STATUS](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support#mbimcidmstransmissionstatus)します。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)

[**NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status)
