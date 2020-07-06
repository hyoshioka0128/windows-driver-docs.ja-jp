---
title: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
description: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
ms.assetid: 6EBC0131-F2EF-4A2D-997A-8990E53369CF
ms.date: 02/11/2019
keywords:
- Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0a6a44f2da4ee51cabb722e442f7b24a86c1a6a1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968317"
---
# <a name="ndis_status_wdi_indication_request_ftm_complete"></a>NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE

ミニポートドライバーは、 [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)のタスクの完了を示す**NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE**状態をホストに送信します。 この通知には、要求された各ターゲットから受信した詳細なタイミング測定 (FTM) 応答の一覧が含まれています。

## <a name="payload-data"></a>ペイロードデータ

| Type | TLV | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- |--- | --- | --- |
| WDI_STATUS | ヘッダー内のフィールド。  |   | イベントの一般的な完了ステータス。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | 複数の TLV\<WDI_TLV_FTM_RESPONSE> | X |   | 各ターゲットの FTM 応答の一覧。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1903

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi

