---
title: ターゲット アプリケーションへの再アタッチ
description: ターゲット アプリケーションへの再アタッチ
ms.assetid: cc137185-58a7-44bf-b262-2698c46730f6
keywords:
- 再ターゲット アプリケーションへのアタッチ
- プロセスにデバッガーを再アタッチ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d905d9f297174bb6a6583ee83a2de207806d1b5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578815"
---
# <a name="reattaching-to-the-target-application"></a>ターゲット アプリケーションへの再アタッチ


## <span id="ddk_re_attaching_to_the_target_application_dbg"></span><span id="DDK_RE_ATTACHING_TO_THE_TARGET_APPLICATION_DBG"></span>


デバッガーがフリーズまたはそれ以外の場合、応答を停止する場合 (つまり、*クラッシュ*) ユーザー モードのデバッグを実行中には、既存のプロセスに新しいデバッガーをアタッチすることができます。

**注**  このメソッドは、Microsoft Windows XP および Windows の以降のバージョンでのみサポートされます。 このメソッドは、かどうか、デバッガー最初プロセスを作成または既存のプロセスにアタッチされているは依存しません。 このメソッドが使用するかどうかに依存しない、 **-pd**オプション。

 

デバッガーを既存の対象アプリケーションに再度アタッチするには、次の操作を行います。

1.  [プロセス ID を特定](finding-the-process-id.md)対象アプリケーションの。

2.  CDB または WinDbg の新しいインスタンスを起動します。 使用して、 **-pe**コマンド ライン オプション。

    ```console
    Debugger -pe -p PID 
    ```

    その他を使用することもできます[コマンド ライン オプション](command-line-options.md)します。

    使用して休止中のデバッガーから接続することもできます、 [ **.attach (プロセスにアタッチ)** ](-attach--attach-to-process-.md)コマンドと共に、 **-e**オプション。

3.  アタッチが完了した後は、元のデバッガー プロセスを終了します。

4.  プロセスが適切に応答しない場合が大きすぎる中断カウントがあります。 使用することができます、 [ **~ (スレッドの再開) m** ](-m--resume-thread-.md)コマンド、中断の数を減らします。 詳細については、中断カウントを参照してください[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

元のデバッガーが正常に動作しても、このメソッドが動作しないがあります。 2 つのデバッガーがデバッグ イベントは、競合して、Windows オペレーティング システムが必ずしもすべてのデバッグ イベントに割り当てない、新しいデバッガー。

新しいデバッガーをアタッチする前に、元のデバッガーは終了しましたが、対象アプリケーションも閉じられます。 (ただしで、デバッガーがアタッチされている場合、 **-pd**オプションと 終了通常は、ターゲット アプリケーションの実行が継続します。 このような状況では、2 つ目のデバッガーをアタッチできます対象アプリケーションを使用せず、 **-pe**オプション)。

プロセスのデバッグは既にデバッグ状態で固定されていることを使用するは残しておくにプロセスからデタッチする場合、 [ **.abandon (破棄プロセス)** ](-abandon--abandon-process-.md)コマンド。 このコマンドの後、Windows デバッガーはこのトピックで説明されている手順を使用してプロセスに再接続できます。

 

 




