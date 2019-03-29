---
title: プロセス ID の検索
description: プロセス ID の検索
ms.assetid: 963e9b5b-2b88-41b5-a103-dc4611ff41ea
keywords:
- プロセス、プロセス ID (PID)
- PID (プロセス ID)
- TList、関連する技術
- タスク マネージャー
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2add0a5362e6f9bbadf0fdddbc464c7cda144d02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579859"
---
# <a name="finding-the-process-id"></a>プロセス ID の検索


## <span id="ddk_finding_the_process_id_dbg"></span><span id="DDK_FINDING_THE_PROCESS_ID_DBG"></span>


Microsoft Windows で実行されている各プロセスと呼ばれる一意の 10 進数が割り当てられて、*プロセス ID*、または*PID*します。 この数は、プロセスを指定して、デバッガーがアタッチするときに使用されます。

特定のアプリケーションの PID を決定するいくつかの方法があります: を使用して、タスク マネージャーを使用して、 **tasklist**コマンド、TList ユーティリティを使用して、またはデバッガーを使用します。

### <a name="span-idtaskmanagerspanspan-idtaskmanagerspantask-manager"></a><span id="task_manager"></span><span id="TASK_MANAGER"></span>タスク マネージャー

*タスク マネージャー*さまざまな方法でアクティブにすることがありますが、CTRL + ALT + DEL キーを押して、クリックして、最も簡単なは**タスク マネージャー**します。

**プロセス** タブで、をクリックして、**詳細** タブに、その他の有用な情報と共に、PID を参照してください。

カーネルの一部のエラーは、タスク マネージャーのグラフィカル インターフェイスで遅延を引き起こす可能性があります。

### <a name="span-idthetasklistcommandspanspan-idthetasklistcommandspanthe-tasklist-command"></a><span id="the_tasklist_command"></span><span id="THE_TASKLIST_COMMAND"></span>Tasklist コマンド

使用して、 **tasklist**すべてのプロセスや、Pid、さまざまなその他の詳細を表示するコマンド プロンプト ウィンドウからコマンド。

### <a name="span-idtlistspanspan-idtlistspantlist"></a><span id="tlist"></span><span id="TLIST"></span>TList

TList (タスク リスト ビューアー、tlist.exe) は、タスク、またはローカル コンピューターで現在実行中のユーザー モード プロセスの一覧を表示するコマンド ライン ユーティリティです。 TList は、Windows のツールをデバッグ パッケージに含まれます。

TList をコマンド プロンプトから実行すると、一意のプロセス id (PID) 番号によってメモリ内ですべてのユーザー モード プロセスの一覧表示されます。 PID、プロセス名、プロセスごとに表示し、プロセスのウィンドウで、そのウィンドウのタイトル。

詳細については、次を参照してください。 [TList](tlist.md)します。

### <a name="span-idthetlistdebuggercommandspanspan-idthetlistdebuggercommandspanthe-tlist-debugger-command"></a><span id="the__tlist_debugger_command"></span><span id="THE__TLIST_DEBUGGER_COMMAND"></span>.Tlist のデバッガー コマンド

問題のシステムで実行されているユーザー モード デバッガーが既にある場合、 [ **.tlist (プロセス Id の一覧)** ](-tlist--list-process-ids-.md)コマンドはそのシステム上ですべて Pid の一覧に表示されます。

### <a name="span-idcsrssandusermodedriversspanspan-idcsrssandusermodedriversspancsrss-and-user-mode-drivers"></a><span id="csrss_and_user_mode_drivers"></span><span id="CSRSS_AND_USER_MODE_DRIVERS"></span>CSRSS とユーザー モード ドライバー

別のコンピューターで実行されているユーザー モード ドライバーをデバッグするには、クライアント サーバー ランタイム サブシステム (CSRSS) プロセスをデバッグします。 詳細については、次を参照してください。[デバッグ CSRSS](debugging-csrss.md)します。

 

 





