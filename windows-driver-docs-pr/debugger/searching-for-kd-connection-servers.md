---
title: KD 接続のサーバーの検索
description: ネットワーク サーバーで実行されている KD 接続の使用可能なサーバーの一覧を取得するのに -QR コマンド ライン オプションを使用して、KD、CDB またはを使用できます。
ms.assetid: 24ff0e2f-d40a-4f52-91ef-e766b9387a8a
keywords:
- KD 接続のサーバーの Windows デバッグの検索
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Searching for KD Connection Servers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6b1e0f630ea6c62633b081006ea59d199cf0168
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530303"
---
# <a name="searching-for-kd-connection-servers"></a>KD 接続のサーバーの検索


KD、CDB でまたはを使用することができます、 **-QR**ネットワーク サーバーで実行されている KD 接続の使用可能なサーバーの一覧を取得するコマンド ライン オプション。

この一覧は、存在しなくなったサーバーを含めることができますが、これが正常にシャット ダウン--次のいずれかへの接続エラー メッセージが生成されます。 一覧には、サーバーとプロセス サーバーのユーザー モードのデバッグも含まれます。 各ケースで、サーバーの種類が示されます。

この構文は次のとおりです。

```console
Debugger -QR \\Server 
```

## <span id="ddk_searching_for_kd_connection_servers_dbg"></span><span id="DDK_SEARCHING_FOR_KD_CONNECTION_SERVERS_DBG"></span>


*デバッガー* KD または CDB できます - いずれの場合も同じ表示になります。 2 つの円記号 (**\\\\**) 前*Server*は省略可能です。

使用することができます、WinDbg で、**スタブのリモート サーバーへの接続**使用可能な KD 接続のサーバーの一覧を参照するダイアログ ボックス。 参照してください[ファイル |リモートのスタブに接続する](file---connect-to-remote-stub.md)の詳細。

**注**  こと、KD 接続サーバー検出可能にするのには、昇格した特権でアクティブ必要があります。 詳細については、[KD 接続のサーバーをアクティブ化する](activating-a-kd-connection-server.md)を参照してください。

 

**注**  サーバー コンピューターにアクセス権を持つアカウントを使用してクライアント コンピューターにログオンしていない場合は、ユーザー名とパスワードを指定するは必要です。 クライアント コンピューターでは、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**net \\ \\**  <em>Server</em>**\\ipc$/user:**<em>UserName</em>場所*Server*、サーバー コンピューターの名前を指定し、*ユーザー名*をサーバー コンピューターへのアクセスを持つアカウントの名前を指定します。

メッセージが表示されたらのパスワードを入力します。 *UserName*します。

このコマンドが成功した後を使用して KD 接続のサーバー (サーバーのコンピューターで実行されている) を検出できます **-QR**または**リモート スタブへの接続**します。

 

 

 





