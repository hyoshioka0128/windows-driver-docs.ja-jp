---
title: NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS
description: ミニポート ドライバーでは、モバイル ブロード バンド (MB) のサービスに以前 OID_WWAN_SAR_TRANSMISSION_STATUS クエリまたは一連の要求の完了を通知するために、NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 通知を使用します。
ms.assetid: 0F04AC31-A16F-4E6A-A5FF-A69574A300A1
ms.date: 08/20/2018
keywords: -NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7b8250b6494324f0f13f1eb838ed3d39ca27c637
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372208"
---
# <a name="ndisstatuswwansartransmissionstatus"></a>NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS

ミニポート ドライバーを使用して、 **NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS**モバイル ブロード バンド (MB) のサービスに前回の完了を通知するために通知[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)クエリまたは要求を設定します。

要請されていないイベントは、アクティブな無線 (OTA) チャネルへの変更がある場合に送信されます。 たとえば、モデムには、パケット データのアップロードが開始されている場合、ペイロードをアップロードできるように、ネットワークのデータ チャネルを使用する場合に、アップリンク チャネルを設定する必要があります。 これにより、オペレーティング システムに提供される通知がトリガーされます。

この通知を使用して、 [ **NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_TRANSMISSION_STATUS_info)構造体。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 Version 1703 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB SAR プラットフォームのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)
