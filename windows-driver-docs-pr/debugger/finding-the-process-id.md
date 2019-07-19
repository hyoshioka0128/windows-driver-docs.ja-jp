---
title: プロセス ID の検索
description: プロセス ID の検索
ms.assetid: 963e9b5b-2b88-41b5-a103-dc4611ff41ea
keywords:
- プロセス、プロセス ID (PID)
- PID (プロセス ID)
- Tlist.exe、関連技術
- タスク マネージャー
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7a1adf48b784948e13a3e962fa96e0c08993d77a
ms.sourcegitcommit: b9a65cb309bea3d35048968bdc708e0067276e68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68313216"
---
# <a name="finding-the-process-id"></a>プロセス ID の検索


## <span id="ddk_finding_the_process_id_dbg"></span><span id="DDK_FINDING_THE_PROCESS_ID_DBG"></span>


Microsoft Windows で実行されている各プロセスには、プロセス ID (PID) と呼ばれる一意の10進数が割り当てられます。 この数値は、デバッガーをアタッチするときのプロセスを指定するために使用されます。

タスクマネージャー、 **tasklist**コマンド、tlist.exe ユーティリティ、またはデバッガーを使用して、特定のアプリの PID を特定できます。

## <a name="span-idtaskmanagerspanspan-idtaskmanagerspantask-manager"></a><span id="task_manager"></span><span id="TASK_MANAGER"></span>タスクマネージャー

タスクマネージャーはさまざまな方法で開くことができますが、最も簡単な方法は、Ctrl + Alt + Del キーを押してから **[タスクマネージャー]** を選択することです。

**[プロセス]** タブで、 **[詳細]** を選択して、PID とその他の有用な情報を確認します。

カーネルエラーによっては、タスクマネージャーのグラフィカルインターフェイスで遅延が発生することがあります。

## <a name="span-idthetasklistcommandspanspan-idthetasklistcommandspanthe-tasklist-command"></a><span id="the_tasklist_command"></span><span id="THE_TASKLIST_COMMAND"></span>**Tasklist**コマンド

コマンドプロンプトから**tasklist**コマンドを使用して、すべてのプロセス、その pid、およびその他のさまざまな詳細を表示します。

## <a name="span-idtlistspanspan-idtlistspantlist-utility"></a><span id="tlist"></span><span id="TLIST"></span>Tlist.exe ユーティリティ

タスク一覧ビューアー (Tlist.exe) または tlist.exe は、ローカルコンピューターで現在実行されているタスクまたはユーザーモードプロセスの一覧を表示するコマンドラインユーティリティです。 Tlist.exe は、Windows 用デバッグツールパッケージに含まれています。

コマンドプロンプトから Tlist.exe を実行すると、メモリ内のすべてのユーザーモードプロセスの一覧が一意の PID 番号と共に表示されます。 プロセスごとに、PID、プロセス名、およびプロセスにウィンドウがある場合はそのウィンドウのタイトルが表示されます。

詳細については、「 [tlist.exe](tlist.md)」を参照してください。

## <a name="span-idthetlistdebuggercommandspanspan-idthetlistdebuggercommandspanthe-tlist-debugger-command"></a><span id="the__tlist_debugger_command"></span><span id="THE__TLIST_DEBUGGER_COMMAND"></span>**Tlist.exe**デバッガーコマンド

問題のシステムで実行されているユーザーモードのデバッガーが既に存在する場合は、 [**tlist.exe (List IDs)** ](-tlist--list-process-ids-.md)コマンドを実行すると、そのシステムのすべての pid の一覧が表示されます。

## <a name="span-idcsrssandusermodedriversspanspan-idcsrssandusermodedriversspancsrss-and-user-mode-drivers"></a><span id="csrss_and_user_mode_drivers"></span><span id="CSRSS_AND_USER_MODE_DRIVERS"></span>CSRSS およびユーザーモードドライバー

別のコンピューターで実行されているユーザーモードドライバーをデバッグするには、クライアントサーバーの実行時サブシステム (CSRSS) プロセスをデバッグします。 詳細については、「 [CSRSS のデバッグ](debugging-csrss.md)」を参照してください。

 

 





