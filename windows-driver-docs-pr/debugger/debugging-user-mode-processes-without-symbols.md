---
title: シンボルを使用しないユーザーモード プロセスのデバッグ
description: シンボルを使用しないユーザーモード プロセスのデバッグ
ms.assetid: ac742239-ed6b-4813-80d6-7b8eb84a0cb4
keywords:
- シンボル、シンボルを使用しないデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed71b1003b1a5f0667b8ae89bdf02ef0a18c40de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346366"
---
# <a name="debugging-user-mode-processes-without-symbols"></a>シンボルを使用しないユーザーモード プロセスのデバッグ


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


エラーをユーザー モード デバッガーを開始する前にエラーが発生したコンピューター上のシンボルに重要です。 ただし、場合によって、デバッガーが開始されますシンボルのないです。 問題が簡単に再現可能な場合は、シンボルをコピーし、再実行してください。 ただし、問題が再度発生しない可能性がある場合は、いくつかの情報も、障害から得られます。

1.  アドレスとはどのような意味を把握するには、エラーに 1 つに一致するコンピューターを必要があります。 同じプラットフォーム (x86 または x64) と同じバージョンの Windows で読み込むことが、必要があります。

2.  構成されたコンピューターがある場合は、ユーザー モード シンボルと新しいコンピューターにデバッグするバイナリをコピーします。

3.  シンボルのないコンピューターで、CDB または WinDbg を起動します。

4.  シンボルのないコンピューターでどのアプリケーションが失敗しましたがわからない場合は、発行、 [ **|(プロセスの状態)** ](---process-status-.md)コマンド。 名前を指定しない、シンボルのないコンピューターの KD を分割し、操作を[ **! process 0 0**](-process.md)、CDB コマンドで指定されたプロセス ID を探し求めています。

5.  2 つのデバッガーを設定する - していない、エラーをヒットするシンボルを使用した 1 つと、エラーがヒットがシンボルなしは、1 つの問題がある場合、 [ **k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)シンボルのないコマンドマシン。

6.  シンボルを使用したマシンで、発行、 [ **u (Unassemble)** ](u--unassemble-.md)のシンボルのないスタックで指定された各アドレス コマンド。 こうスタック トレースのシンボルのないコンピューターでエラーが発生します。

7.  スタック トレースを調べることで、呼び出しに関連するモジュールと関数の名前を確認できます。

 

 





