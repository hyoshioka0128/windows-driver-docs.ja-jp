---
title: GUID_NDIS_STATUS_OPER_STATUS
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_STATUS_OPER_STATUS GUID について説明します。
ms.assetid: e4e13f9d-6298-47b0-9cb1-70fea87db59a
keywords:
- GUID_NDIS_STATUS_OPER_STATUS、WDK GUID_NDIS_STATUS_OPER_STATUS ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: b081821c516cd345c75bcfa97affad4490528c90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842374"
---
# <a name="guid_ndis_status_oper_status"></a>GUID_NDIS_STATUS_OPER_STATUS

GUID_NDIS_STATUS_OPER_STATUS イベント GUID は、NDIS ネットワークインターフェイスの現在の動作状態を示します。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

Ndis は、NDIS ネットワークインターフェイスの現在の動作状態を報告する[NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)ステータスを生成します。

Ndis が NDIS ネットワークインターフェイスの現在の動作状態の変更を示している場合、NDIS は、WMI クライアントの WMI GUID_NDIS_STATUS_OPER_STATUS イベントに状態の表示も変換します。

NDIS が GUID と共に提供するデータバッファーには、 [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)構造体の後に[NDIS_OPER_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_oper_state)構造体が含まれています。 使用可能な値の一覧については、「 [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)」を参照してください。

