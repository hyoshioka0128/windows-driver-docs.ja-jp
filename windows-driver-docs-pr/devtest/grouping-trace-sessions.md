---
title: トレース セッションのグループ化
description: トレース セッションのグループ化
ms.assetid: dd9f39ee-fb93-4bf8-ac5c-5e884e57fcaa
keywords:
- Traceview で WDK、セッションをグループ化
- トレース セッションをグループ化
- WDK、グループのセッションをトレースします。
- WDK traceview で複数のトレース セッション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5213575fba7d6ed92ed494d1350dfaca87d28bf5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360392"
---
# <a name="grouping-trace-sessions"></a>トレース セッションのグループ化


複数の実行中のトレース セッションを組み合わせたり、トレース セッションのグループに複数の既存のトレース ログを表示します。 グループ化されたセッションからのトレース メッセージとログは、1 つにまとめて表示されます。[トレース メッセージ一覧](trace-message-lists.md)ウィンドウ。

トレース セッションのグループは、1 つのセッションとして管理されます。 たとえば、グループの一部であるトレース セッションを停止すると、traceview では、グループ内のすべてのトレース セッションを停止します。 同様に場合、する[トレース メッセージをフィルター処理](filtering-trace-messages.md)グループ内のすべてのトレース メッセージにフィルターが適用されます。 ただし、グループの一部である、まだ 1 つのトレース セッションまたはそのプロバイダーのプロパティを変更することができます。

トレース セッションのグループ化には影響しません、[イベント トレース ログ (.etl) ファイル](trace-log.md)、traceview でのトレース セッション (.out) ファイル、または traceview での概要 (.sum) ファイルを一覧表示します。 これらのファイルは、セッションがグループ化されていない場合と同様、各セッションのデータを記録します。

このセクションの内容:

[トレース セッションのグループを作成します。](creating-trace-session-groups.md)

[トレース セッションをグループ化の解除](ungrouping-trace-sessions.md)

[グループのログを保存しています](saving-a-group-log.md)

[グループ化の制限事項](limitations-of-grouping.md)

 

 





