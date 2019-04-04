---
title: デバッグ セッションの開始
description: デバッグ セッションの開始
ms.assetid: 789c61cf-edd2-4354-91a8-87a0a7af28a3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d46944dc9ab0a023a90198f527b5bace5be7d139
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527814"
---
# <a name="starting-the-debugging-session"></a>デバッグ セッションの開始


## <span id="ddk_opening_a_crash_dump_dbg"></span><span id="DDK_OPENING_A_CRASH_DUMP_DBG"></span>


方法に関するこのドキュメントで[カーネル デバッガーからユーザー モードのデバッグを制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)、*ターゲット アプリケーション*はデバッグ中は、ユーザー モード アプリケーションを*対象のコンピュータ*ターゲット アプリケーションと、CDB、NTSD、またはプロセスを格納しているコンピューターを参照し、*ホスト コンピューター*カーネル デバッガーを格納しているコンピューターを参照します。

この手法の使用を開始するには、次の操作を行う必要があります。 手順 1. および 2. は任意の順序で行うことができます。

1. -D コマンド ライン オプションを使用して、対象のコンピューターか CDB、NTSD を起動します。

   たとえば、次の構文を使用して実行中のプロセスにアタッチできます。

   **ntsd -d \[-y** <em>UserSymbolPath</em>**\] -p** *PID*

   または、次の構文を使用して、ターゲットとして、新しいプロセスを開始できます。

   **ntsd -d \[-y** <em>UserSymbolPath</em>**\]** *ApplicationName*

   これをインストールする事後分析をデバッガーとして場合、は、次の構文を使用します。

   **ntsd -d \[-y** <em>UserSymbolPath</em>**\]**

   この手順の詳細については、[デバッグ ユーザー モード プロセスを使用して CDB](debugging-a-user-mode-process-using-cdb.md)を参照してください。

2. まるで、対象のコンピューターをデバッグしようとしていたが、実際に損なわれないターゲット コンピューターに、ホスト コンピューターでは、WinDbg または KD を起動します。 WinDbg を使用するには、次の構文を使用します。

   **windbg \[-y** <em>KernelSymbolPath</em>**\] \[-k** <em>ConnectionOptions</em>**\]**

   この手順の詳細については、[Live カーネル モードのデバッグを使用して WinDbg](performing-kernel-mode-debugging-using-windbg.md)を参照してください。

   **注**WinDbg の使い慣れた機能の多くはこのシナリオでは利用できませんカーネル デバッガーとして WinDbg を使用する場合。 たとえば、ローカル ウィンドウ、逆アセンブル ウィンドウまたは呼び出し履歴 ウィンドウを使用することはできませんし、ソース コードをステップすることはできません。 これは、(NTSD または CDB)、デバッガーのビューアーとして WinDbg がのみ機能するため、ターゲット コンピューターで実行します。

     

3. ユーザー モードのシンボル パスを設定していない場合は、入力から設定&gt;プロンプト。 カーネル モードのシンボル パスを設定していない場合は、kd から設定&gt;プロンプト。 これらのプロンプトにアクセスして、モードを切り替える方法については、[モードの切り替え](switching-modes.md)を参照してください。

CDB を使用する場合 CDB に関連付けられているコマンド プロンプト ウィンドウでデバッグが続行中にロックされ、使用できないが残ります。 NTSD を使用する場合は、追加のウィンドウは作成されません、NTSD でターゲット コンピューターに関連付けられているプロセス ID も。

ユーザー モード デバッガーを実行するかどうか、カーネル デバッガー中もデバッグ サーバーとして使用するを参照してください[リモート デバッグをこのメソッドを組み合わせて](combining-this-method-with-remote-debugging.md)します。

 

 





