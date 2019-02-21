---
title: 16 の例をデバッガーでのトレース メッセージの表示
description: 16 の例をデバッガーでのトレース メッセージの表示
ms.assetid: c548643c-ae0c-47e7-af0a-0d89ed78f281
keywords:
- WDK を表示するトレース メッセージ
- トレース メッセージを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 393da6d1968da18c793ce9000a441c546d03e067
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527768"
---
# <a name="example-16-viewing-trace-messages-in-a-debugger"></a>16 の使用例:デバッガーでのトレース メッセージの表示


## <span id="ddk_viewing_trace_messages_in_a_debugger_tools"></span><span id="DDK_VIEWING_TRACE_MESSAGES_IN_A_DEBUGGER_TOOLS"></span>


この例では、WinDbg、KD にトレース メッセージをリダイレクトする方法を示します。

トレース セッションを開始する前に Wmitrace.dll と Traceprt.dll がホスト コンピューターで、デバッガーの検索パスを確認します。 これらの Dll が含まれている[ツールを Windows のデバッグ](https://go.microsoft.com/fwlink/p/?linkid=8708)で、 \\Program Files\\ツールを Windows のデバッグ\\winxp ディレクトリ。 (ディレクトリの名前に関係なく、ファイル操作 Windows 2000 と Windows の以降のバージョン)。

また、いることを確認、[トレース メッセージの形式のファイル](trace-message-format-file.md)(TMF) トレース プロバイダーは、デバッガーの検索パス。

デバッガーの検索パスを設定するには、使用、! wmitrace.searchpath デバッガー拡張機能を特殊化または % のトレースの値を設定\_形式\_検索\_%path% 環境変数。 次に、例を示します。

```
set TRACE_FORMAT_SEARCH_PATH=c:\tracing
```

次に、デバッガーを起動します。 トレース ログのコマンドを送信する場合、 **-kd**パラメーター、およびデバッガーが実行されていない、トレース ログが応答しなくなる (「ハングアップ」)。

次のコマンドは、トレース セッションを開始し、Windbg、KD からか、トレース メッセージを送信しますがアタッチされているいずれか。

```
tracelog -start MyTrace -guid MyProvider.ctl -rt -kd
```

**Tracelog-開始**コマンドには、トレース セッションを開始するセッションの名前が含まれています。 使用して、 **- guid**プロバイダー ファイルを識別するパラメーター。 また、使用、 **-rt**デバッガーとログ ファイルにトレース メッセージが送信されるように、リアルタイムのトレース セッションを開始するパラメーター。

応答では、トレース ログは、セッションが開始されたことを報告します。 トレース プロバイダーは、メッセージを生成するときは、デバッガーで、メッセージが表示されます。

デバッガーでのメッセージを表示するには、WMI のトレース拡張機能を使用します。 詳しくは、次を参照してください。[ツールを Windows のデバッグ](https://go.microsoft.com/fwlink/p/?linkid=8708)します。

 

 





