---
title: プロセス サーバーの検索
description: ネットワーク サーバーのコンピューターで実行されている利用可能なプロセス サーバーの一覧を取得するのに -QR コマンド ライン オプションを使用して、KD、CDB またはを使用できます。
ms.assetid: 2f0cd4df-f18a-4222-ab90-7aba0f177eff
keywords:
- デバッグ プロセス サーバーの Windows の検索
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Searching for Process Servers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 652878d1ba1423eca72285f7f4651fc56e557b35
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382001"
---
# <a name="searching-for-process-servers"></a>プロセス サーバーの検索


KD、CDB でまたはを使用することができます、 **-QR**ネットワーク サーバーのコンピューターで実行されている利用可能なプロセス サーバーの一覧を取得するコマンド ライン オプション。

この一覧は、存在しなくなったサーバーを含めることができますが、これが正常にシャット ダウン--次のいずれかへの接続エラー メッセージが生成されます。 一覧では、サーバーと KD 接続のサーバーのデバッグも含まれます。 各ケースで、サーバーの種類が示されます。

この構文は次のとおりです。

```console
Debugger -QR \\Server
```

## <span id="ddk_searching_for_process_servers_dbg"></span><span id="DDK_SEARCHING_FOR_PROCESS_SERVERS_DBG"></span>


*デバッガー* KD または CDB できます - いずれの場合も同じ表示になります。 2 つの円記号 (**\\\\**) 前*Server*は省略可能です。

使用することができます、WinDbg で、**スタブのリモート サーバーへの接続**利用可能なプロセス サーバーの一覧を参照するダイアログ ボックス。 参照してください[ファイル |リモートのスタブに接続する](file---connect-to-remote-stub.md)の詳細。

**注**  が、検出可能にプロセス サーバーは、昇格した特権でアクティブ必要があります。 詳細については、次を参照してください。[プロセス サーバーをアクティブ化する](activating-a-process-server.md)します。

 

**注**  サーバー コンピューターにアクセス権を持つアカウントを使用してクライアント コンピューターにログオンしていない場合は、ユーザー名とパスワードを指定するは必要です。 クライアント コンピューターでは、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**net \\ \\**  <em>Server</em>**\\ipc$/user:**<em>UserName</em>場所*Server*、サーバー コンピューターの名前を指定し、*ユーザー名*をサーバー コンピューターへのアクセスを持つアカウントの名前を指定します。

メッセージが表示されたらのパスワードを入力します。 *UserName*します。

このコマンドが成功した後を使用して (サーバーのコンピューターで実行されている) プロセス サーバーを検出できます **-QR**または**リモート スタブへの接続**します。

 


 