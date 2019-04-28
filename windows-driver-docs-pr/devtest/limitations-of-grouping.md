---
title: グループ化の制限事項
description: グループ化の制限事項
ms.assetid: 2cc49522-a504-43d7-b36b-297cd6c3f307
keywords:
- トレース セッションをグループ化
- WDK、グループのセッションをトレースします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 248124b5f9863e0b256ce13bd3577013ae3590fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369750"
---
# <a name="limitations-of-grouping"></a>グループ化の制限事項

このトピックでは、traceview でグループ化機能の制限事項について説明します。

### <a name="span-idworkspacesandgroupsspanspan-idworkspacesandgroupsspanworkspaces-and-groups"></a><span id="workspaces_and_groups"></span><span id="WORKSPACES_AND_GROUPS"></span>ワークスペースとグループ

ワークスペースでトレース セッションのグループを保存することはできません。 Traceview で表示する「設定を保存できませんワークスペースのグループ化されたセッションです」しようとすると、 エラー メッセージ.

### <a name="span-idremovingtracesessiongroupsspanspan-idremovingtracesessiongroupsspanremoving-trace-session-groups"></a><span id="removing_trace_session_groups"></span><span id="REMOVING_TRACE_SESSION_GROUPS"></span>トレース セッションのグループを削除します。

トレース セッションでグループを削除することはできません、[トレース セッション リスト](trace-session-list.md)グループ内のすべてのセッションが停止された場合でも、します。 グループを削除する前に、トレース セッションを解除する必要があります。

### <a name="span-idtracemessageorderinagroupspanspan-idtracemessageorderinagroupspantrace-message-order-in-a-group"></a><span id="trace_message_order_in_a_group"></span><span id="TRACE_MESSAGE_ORDER_IN_A_GROUP"></span>グループ内のトレース メッセージの順序

トレース セッションの一覧で、トレース メッセージの到着が各トレース セッションのメッセージの頻度、バッファー サイズ、およびフラッシュ タイマーによって影響を受けるため、同時に到着する別のセッションからのトレース メッセージ実際に発生した可能性に非常に異なる時間。 正確なビューでは、各トレース セッションの出力ファイルを組み合わせて使用してで並べ替えて、**システム時刻**列。
