---
title: デバッグ サーバーの検索
description: ネットワーク サーバーで実行されている使用可能なデバッグ サーバーの一覧を取得するのに -QR コマンド ライン オプションを使用して、KD、CDB またはを使用できます。
ms.assetid: 510d5f9a-cde8-4dc8-8e2f-80f84ad44fce
keywords:
- デバッグ サーバーの Windows をデバッグするための検索
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Searching for Debugging Servers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e3dfbf210bd28e7ff008da18015e0f24d95af58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578194"
---
# <a name="searching-for-debugging-servers"></a>デバッグ サーバーの検索


KD、CDB でまたはを使用することができます、 **-QR**ネットワーク サーバーで実行されている使用可能なデバッグ サーバーの一覧を取得するコマンド ライン オプション。

この一覧は、存在しなくなったサーバーを含めることができますが、これが正常にシャット ダウン--次のいずれかへの接続エラー メッセージが生成されます。 一覧には、プロセス サーバーと KD 接続サーバーも含まれます。 各ケースで、サーバーの種類が示されます。

この構文は次のとおりです。

```console
Debugger -QR \\Server 
```

## <span id="ddk_searching_for_debugging_servers_dbg"></span><span id="DDK_SEARCHING_FOR_DEBUGGING_SERVERS_DBG"></span>


*デバッガー* KD または CDB できます - いずれの場合も同じ表示になります。 2 つの円記号 (**\\\\**) 前*Server*は省略可能です。

使用することができます、WinDbg で、**リモート デバッガー セッションへの接続**使用可能なサーバーの一覧を参照するダイアログ ボックス。 参照してください[ファイル |リモート セッションに接続する](file---connect-to-remote-session.md)詳細についてはします。

**注**  こと、デバッグ サーバーを検出するには、昇格した特権でアクティブ必要があります。 詳細については、次を参照してください。[デバッグ サーバー アクティブ化する](activating-a-debugging-server.md)します。

 

**注**  サーバー コンピューターにアクセス権を持つアカウントを使用してクライアント コンピューターにログオンしていない場合は、ユーザー名とパスワードを指定するは必要です。 クライアント コンピューターでは、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**net \\ \\**  <em>Server</em>**\\ipc$/user:**<em>UserName</em>場所*Server*、サーバー コンピューターの名前を指定し、*ユーザー名*をサーバー コンピューターへのアクセスを持つアカウントの名前を指定します。

メッセージが表示されたらのパスワードを入力します。 *UserName*します。

このコマンドが成功した後を使用して (サーバーのコンピューターで実行されている) デバッグのサーバーを検出できます **-QR**または**リモート デバッガー セッションへの接続**します。

 

 

 





