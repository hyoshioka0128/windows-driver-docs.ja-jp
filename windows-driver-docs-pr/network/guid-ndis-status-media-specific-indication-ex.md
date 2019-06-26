---
title: GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX について説明します。
ms.assetid: 34839471-5b3b-4a95-a610-bc35e7774c14
keywords:
- GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX、WDK GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc108e8d1d2b64e00215c15b7d3edc3152b6b2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382683"
---
# <a name="guidndisstatusmediaspecificindicationex"></a>GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX

GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX イベント GUID では、メディア固有の状態を示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

ミニポート ドライバーでは、メディア固有の状態を示します、NDIS は、WMI GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX を示す値を WMI クライアントの状態表示を変換します。

ミニポート ドライバーでは、メディア固有の状態インジケーターを行う呼び出すことによって、 [NdisMIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)関数と、 **StatusCode**のメンバー、 [NDIS_STATUS_INDICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体、 *StatusIndication*パラメーターが指す NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX に設定します。 **StatusBuffer**この構造体のメンバーがで指定されている状態の表示に固有の形式でデータが含まれるドライバーに割り当てられたバッファーを指す**StatusCode**します。

、特定のメディアを示す値の種類に応じて GUID ヘッダーをメディアに固有の表示に固有のデータを後に可能性があります。 この GUID を持つ NDIS を提供するデータ バッファーが含まれています、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)存在する場合、メディア固有のデータは後に構造体。

