---
title: プロセスとスレッドの制御
description: プロセスとスレッドの制御
ms.assetid: f5a50b54-443e-425e-98cb-cff8d31ac897
keywords:
- プロセス
- 選択が処理します。
- スレッド (thread)
- スレッドの選択
- スレッドを凍結
- スレッドを解除する (凍結解除)
- スレッドの中断
- スレッドの中断回数
- スレッドを凍結
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21fafe94ccd6d6b262b2505cc00b83ff640a3209
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375064"
---
# <a name="controlling-processes-and-threads"></a>プロセスとスレッドの制御


## <span id="ddk_controlling_processes_and_threads_dbg"></span><span id="DDK_CONTROLLING_PROCESSES_AND_THREADS_DBG"></span>


ユーザー モードを実行している場合、デバッグするアクティブ化、表示、固定、固定の解除、中断、およびプロセスとスレッドを停止解除。

*現在*または*active*プロセスはプロセスは、現在デバッグ中です。 同様に、*現在*または*active*スレッドはスレッド、デバッガーが現在制御です。 多くのデバッガー コマンドの操作は、現在のプロセスとスレッドの id によって決まります。 現在のプロセスには、デバッガーが使用する仮想アドレスへのマッピングも決定します。

デバッグの開始時に、現在のプロセスに、デバッガーがアタッチされている、またはデバッガーに割り込んだ例外の原因となったものになります。 同様に、現在のスレッドが、デバッガーがプロセスにアタッチされているか、例外の原因となったときにアクティブだった 1 つです。 ただし、デバッガーを使用して、現在のプロセスとスレッドを変更および固定または個々 のスレッドの固定を解除することができます。

カーネル モードで、デバッグのプロセスとスレッドによって制御されないこのセクションで説明されているメソッド。 カーネル モードでのプロセスとスレッドを操作する方法の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

### <a name="span-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspandisplaying-processes-and-threads"></a><span id="displaying_processes_and_threads"></span><span id="DISPLAYING_PROCESSES_AND_THREADS"></span>プロセスとスレッドを表示します。

プロセスとスレッドの情報を表示するには、次のメソッドを使用できます。

-   [ **|(プロセスの状態)** ](---process-status-.md)コマンド

-   [ **~ (スレッド ステータス)** ](---thread-status-.md)コマンド

-   (WinDbg のみ)[プロセスとスレッド ウィンドウ](processes-and-threads-window.md)

### <a name="span-idsettingthecurrentprocessandthreadspanspan-idsettingthecurrentprocessandthreadspansetting-the-current-process-and-thread"></a><span id="setting_the_current_process_and_thread"></span><span id="SETTING_THE_CURRENT_PROCESS_AND_THREAD"></span>現在のプロセスとスレッドの設定

現在のプロセスまたはスレッドを変更するには、次のメソッドを使用できます。

-   [ **| S (現在のプロセスの設定)** ](-s--set-current-process-.md)コマンド

-   [ **~ (設定現在のスレッド) s** ](-s--set-current-thread-.md)コマンド

-   (WinDbg のみ)[プロセスとスレッド ウィンドウ](processes-and-threads-window.md)

### <a name="span-idfreezingandsuspendingthreadsspanspan-idfreezingandsuspendingthreadsspanfreezing-and-suspending-threads"></a><span id="freezing_and_suspending_threads"></span><span id="FREEZING_AND_SUSPENDING_THREADS"></span>固定して、スレッドの中断

デバッガーによってスレッドの実行を変更できます*中断*スレッドまたは*フリーズ*スレッド。 これら 2 つのアクションでは、若干異なる影響があります。

各スレッドで、*中断回数*それに関連付けられています。 この数が 1 つ場合、以上の場合、システムでは、スレッドは実行されません。 Count が 0 または下位、システムの場合は、該当する場合に、スレッドを実行します。

通常、各スレッドには、中断カウントが 0 です。 プロセスにアタッチするデバッガーと、は、いずれかでそのプロセスのすべてのスレッドの中断カウントをインクリメントします。 場合は、プロセスからデタッチされますが、デバッガーがすべてデクリメントしていずれかのカウントを中断します。 デバッガーがプロセスを実行すると一時的にデクリメントすべて中断カウントして 1 つ。

次のメソッドを使用して、デバッガーから任意のスレッドの中断カウントを制御できます。

-   [ **~ N (スレッドの中断)** ](-n--suspend-thread-.md)コマンドを指定されたインクリメントを 1 つのスレッドの中断回数。

-   [ **~ M (Resume スレッド)** ](-m--resume-thread-.md)デクリメントのコマンドを 1 つの指定したスレッドの中断回数。

最も一般的な用途は、これらのコマンドを特定のスレッドを発生させるを 2 つのいずれかからカウントを中断します。 デバッガーが実行するか、プロセスからデタッチされると、スレッドは次が 1 つの中断カウントしが、プロセス内の他のスレッドを実行する場合でも中断している、します。

スレッドを中断するには、実行している場合でも[待合室デバッグ](noninvasive-debugging--user-mode-.md)します。

デバッガーこともできます*固定*スレッド。 このアクションは、いくつかの方法で、スレッドの中断に似ています。 ただし、"凍結した"のデバッガー設定です。 Windows オペレーティング システムでは nothing は何も、このスレッドは異なることを認識します。

既定では、すべてのスレッドでは、固定されました。 デバッガーを実行するプロセスが発生する場合に固定されているスレッドは実行されません。 ただし、デバッガー、プロセスからデタッチされますが、すべてのスレッドが解放します。

個々 のスレッドを保持し、保持するには、次のメソッドを使用できます。

-   [ **~ F (スレッドを凍結)** ](-f--freeze-thread-.md)コマンドが指定したスレッドを凍結します。

-   [ **~ U (スレッドの固定の解除)** ](-u--unfreeze-thread-.md)コマンドは、指定したスレッドを凍結します。

いずれの場合も、ターゲット プロセスに属するスレッドは、デバッガーがターゲットに明らかになったときに実行しないでください。 スレッドの中断カウントは、デバッガーはプロセスを実行またはデタッチ場合にのみ、スレッドの動作に影響します。 固定ステータスは、デバッガーはプロセスを実行する場合にのみ、スレッドの動作に影響します。

### <a name="span-idthreadsandprocessesinothercommandsspanspan-idthreadsandprocessesinothercommandsspanthreads-and-processes-in-other-commands"></a><span id="threads_and_processes_in_other_commands"></span><span id="THREADS_AND_PROCESSES_IN_OTHER_COMMANDS"></span>スレッドおよびプロセスの他のコマンド

スレッドの指定子またはその他の多くのコマンドの前に、プロセスの指定子を追加することができます。 詳細については、個々 のコマンドのトピックを参照してください。

追加することができます、 [ **~ e (スレッド固有のコマンド)** ](-e--thread-specific-command-.md)多くのコマンドおよび拡張機能コマンドの前に修飾子。 この修飾子は、指定したスレッドに対して実行するコマンドをによりします。 この修飾子は、コマンドを 1 つ以上のスレッドに適用する場合に特に便利です。 たとえば、次のコマンドを繰り返し、 [ **! gle** ](-gle.md)がデバッグされているすべてのスレッドの拡張機能コマンド。

```dbgcmd
~*e !gle 
```

### <a name="span-idmultiplesystemsspanspan-idmultiplesystemsspanmultiple-systems"></a><span id="multiple_systems"></span><span id="MULTIPLE_SYSTEMS"></span>複数のシステム

デバッガーは、同時に複数のターゲットにアタッチできます。 これらのプロセスがダンプ ファイルを含める場合、または複数のコンピューター上のライブのターゲットを含めると、デバッガーは、システム、プロセス、およびアクションごとにスレッドを参照します。 この種のデバッグの詳細については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

 

 





