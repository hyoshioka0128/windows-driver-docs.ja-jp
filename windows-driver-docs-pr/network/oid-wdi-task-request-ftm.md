---
title: OID_WDI_TASK_REQUEST_FTM
description: 表示されている BSS ターゲットを使用した問題タイミング測定 (FTM) プロシージャを開始する LE OID_WDI_TASK_REQUEST_FTM が発行されます。
ms.assetid: 67E17BD2-9216-43B5-8D1E-C6DF8537D79E
ms.date: 02/08/2019
keywords:
- OID_WDI_TASK_REQUEST_FTM ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e4d4a295aaa71d6bd80ab3dcbcf371ec77809cc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340016"
---
# <a name="oidwditaskrequestftm"></a>OID_WDI_TASK_REQUEST_FTM


**OID_WDI_TASK_REQUEST_FTM**が一覧表示されている BSS ターゲットを持つ細かいタイミング測定 (FTM) プロシージャを開始する LE に発行します。 ターゲットの数は、値の小さい**FTMNumberOfSupportedTargets**、ステーション属性から取得します。

このタスクは、ターゲットを持つすべての FTM セッションが完了した、タイムアウトは有効期限が切れた、またはホストは、操作を中止すると、すぐに実行する必要があります。

このタスクが完了したときに、ドライバーは送信する必要があります、 [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)要求されたターゲットの各 FTM 応答の一覧を含む状態を示す値。

このタスクが完了した後、ポートが良好な状態である必要があり、ホストが新しい一連のターゲットのタスクを再試行すぐに可能性がありますので、新しい FTM 要求を処理できるようにする必要があります。

ターゲットごとに示される場合、場所の構成情報 (LCI) レポートを要求する必要があります。 、指定した場合、LE はターゲットから 1 つを要求する必要があります。 

## <a name="task-parameters"></a>タスク パラメーター

| TLV | 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | UINT32 |   |   | FTM を完了する、ミリ秒単位の最大時間。 タイムアウトは、ターゲットの数を掛けた 150 ミリ秒に設定されます。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | WDI_FTM_TARGET_BSS_ENTRY | x |   | 手順を実行するどの FTM と BSS ターゲットの一覧。 |

## <a name="task-completion-indication"></a>タスクの完了を示す値

[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |
