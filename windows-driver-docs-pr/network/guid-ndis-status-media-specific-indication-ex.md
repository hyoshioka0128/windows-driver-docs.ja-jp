---
title: GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX GUID について説明します。
ms.assetid: 34839471-5b3b-4a95-a610-bc35e7774c14
keywords:
- GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX、WDK GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9deabb69beaeb5691c628e9f48a48dfffc6c4323
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842279"
---
# <a name="guid_ndis_status_media_specific_indication_ex"></a>GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX

GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX イベント GUID は、メディア固有の状態を示します。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

ミニポートドライバーによってメディア固有の状態が示された場合、NDIS は、WMI クライアントの WMI GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX を示す状態を示します。

ミニポートドライバーは、 [Statusindication](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)パラメーターが指す[NDIS_STATUS_INDICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**StatusCode**メンバーで、関数を呼び出して、メディア固有の状態を*示し*ます。を NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX に設定する場合は。 この構造体の**Statusbuffer**メンバーは、ドライバーによって割り当てられたバッファーを指します。このバッファーには、 **StatusCode**で識別される状態の表示に固有の形式のデータが含まれています。

メディア固有の指示の種類によっては、GUID ヘッダーの後に、メディア固有の表示に固有のデータが続きます。 この GUID で NDIS に用意されているデータバッファーには、メディア固有のデータがある場合は、その後に続く[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体が含まれます。

