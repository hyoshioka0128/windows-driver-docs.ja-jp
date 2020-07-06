---
title: OID_WDI_TASK_REQUEST_FTM
description: OID_WDI_TASK_REQUEST_FTM は、リストされている BSS ターゲットを使用して、詳細なタイミング測定 (FTM) プロシージャを開始するために LE に発行されます。
ms.assetid: 67E17BD2-9216-43B5-8D1E-C6DF8537D79E
ms.date: 02/08/2019
keywords:
- Windows Vista 以降のネットワークドライバーの OID_WDI_TASK_REQUEST_FTM
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a7e2cf3a171a59613e11575b7b6c2e9025620856
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968537"
---
# <a name="oid_wdi_task_request_ftm"></a>OID_WDI_TASK_REQUEST_FTM


**OID_WDI_TASK_REQUEST_FTM**は、リストされている BSS ターゲットを使用して、詳細なタイミング測定 (FTM) プロシージャを開始するために LE に発行されます。 ターゲットの数が、ステーション属性から取得された**Ftmnumberofsupportedtargets**の値以下です。

このタスクは、ターゲットを持つすべての FTM セッションが完了するか、タイムアウトが経過するか、ホストが操作を中止した直後に完了する必要があります。

このタスクが完了すると、ドライバーは、要求された各ターゲットの FTM 応答の一覧を含む[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)状態の通知を送信する必要があります。

このタスクが完了したら、ポートは良好な状態であり、新しい FTM 要求を処理する準備ができている必要があります。これは、ホストが新しいターゲットのセットを使用してタスクを直ちに再試行する可能性があるためです。

ターゲットごとに、場所の構成情報 (LCI) レポートを要求するかどうかが示されます。 指定されている場合、LE はターゲットに1つを要求します。 

## <a name="task-parameters"></a>タスク パラメーター

| TLV | Type | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | UINT32 |   |   | FTM を完了するまでの最大時間 (ミリ秒単位)。 タイムアウトは、150ミリ秒にターゲットの数を乗算した値に設定されます。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | WDI_FTM_TARGET_BSS_ENTRY | X |   | FTM の手順を完了する必要がある BSS ターゲットの一覧。 |

## <a name="task-completion-indication"></a>タスクの完了を示す

[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1903

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi

