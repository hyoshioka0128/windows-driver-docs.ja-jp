---
title: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
description: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
ms.assetid: 6EBC0131-F2EF-4A2D-997A-8990E53369CF
ms.date: 02/11/2019
keywords:
- NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 90d173cbabb928e587cadf16c2f8c92855748059
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905439"
---
# <a name="ndisstatuswdiindicationrequestftmcomplete"></a>NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE

ミニポート ドライバーの送信、 **NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE**タスクの完了を示すとしてホストに状態を示す値[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)します。 この通知には、各要求されたターゲットから受け取った問題タイミング測定 (FTM) 応答の一覧が含まれています。

## <a name="payload-data"></a>ペイロード データ

| 種類 | TLV | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- |--- | --- | --- |
| WDI_STATUS | ヘッダー フィールド。  |   | イベントの一般的な完了状態。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | 複数の TLV\<WDI_TLV_FTM_RESPONSE > | x |   | 各ターゲット FTM 応答の一覧。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |
