---
title: ファイアウォールとプロキシ サーバー
description: ファイアウォールとプロキシ サーバー
ms.assetid: 6b438602-299e-4cc5-ac75-ac9ee3cb50bb
keywords:
- SymSrv、ファイアウォールおよびプロキシ サーバー
- ファイアウォールと SymSrv
- インターネット ファイアウォールと SymSrv
- プロキシ サーバーと SymSrv
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0105e789e4c0148c9d58cbb97c8a75deb9e95f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529752"
---
# <a name="firewalls-and-proxy-servers"></a>ファイアウォールとプロキシ サーバー


## <span id="ddk_firewalls_and_proxy_servers_dbg"></span><span id="DDK_FIREWALLS_AND_PROXY_SERVERS_DBG"></span>


SymSrv、シンボルへのアクセスに使用して、コンピューターがプロキシ サーバーを使用するネットワーク上またはシンボル ストアがファイアウォールの外側には、認証が行われるようにデータ転送に必要な場合があります。

SymSrv では、認証要求を受信すると、デバッガーする認証要求を表示するか自動的に構成した方法に応じて、要求を拒否します。

SymSrv には、プロキシ サーバーのサポートが統合されています。 既定のプロキシ サーバーを使用することができますか[SymProxy](symproxy.md)、任意の別のプロキシ サーバーを使用することができます。

### <a name="span-idauthenticationrequestsspanspan-idauthenticationrequestsspanauthentication-requests"></a><span id="authentication_requests"></span><span id="AUTHENTICATION_REQUESTS"></span>認証要求

認証要求を許可するのには、デバッガーを構成できます。 ファイアウォールまたはプロキシ サーバーが承認を要求するとダイアログ ボックスが表示されます。 ある種の情報 (通常はユーザー名とパスワード) を入力する必要があります前に、デバッガーがシンボルをダウンロードできます。 誤った情報を入力すると、ダイアログ ボックスが再表示されます。 選択した場合、**キャンセル**ボタン、ダイアログ ボックスが表示されなくなりますおよびシンボル情報は転送されません。

場合は、デバッガーはダイアログ ボックスは表示されないすべての認証要求を拒否するように構成され、認証が必要な場合は、シンボルは転送されません。

認証要求を拒否するか、デバッガーは、自動的に認証要求を拒否、SymSrv ないことがシンボル ストアの通信を試みます。 連絡先を更新する場合は、デバッグ セッションを再開かを使用して、 [ **! symsrv 閉じます**](-symsrv.md)します。

**注**  認証ダイアログ ボックスが開いているウィンドウの背後に表示される KD、CDB またはを使用している場合。 このような場合は、移動、またはこのダイアログ ボックスを確認するにはいくつかの windows を最小限に抑える必要があります。

 

WinDbg を既定では認証要求が許可されます。 KD、CDB で認証要求は自動的に既定で拒否されました。

認証要求を許可するには、いずれかの操作を使用して[ **! sym プロンプト**](-sym.md)または[ **.symopt 0x80000**](-symopt--set-symbol-options-.md)。 すべての要求を拒否するには、いずれかを使用 **! オフ sym が求められます**または **.symopt + 0x80000**します。 現在の設定を表示する使用 **! sym**します。

使用する必要があります[ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)認証アクセス許可の状態を変更した後。

### <a name="span-idchoosingaproxyserverspanspan-idchoosingaproxyserverspanchoosing-a-proxy-server"></a><span id="choosing_a_proxy_server"></span><span id="CHOOSING_A_PROXY_SERVER"></span>プロキシ サーバーを選択します。

Windows の既定のプロキシ サーバーを選択するには、開く**インターネット オプション**コントロール パネルで、選択、**接続**、タブを選び、 **LAN の設定**ボタンをクリックします。 プロキシ サーバー名とポート番号、または選択を入力することができますし、**詳細**を複数のプロキシ サーバーを構成します。 詳細については、Internet Explorer のヘルプ ファイルを参照してください。

使用する symsrv の特定のプロキシ サーバーを選択するには、設定、 \_NT\_シンボル\_プロキシの環境変数の名前または IP アドレスのプロキシ サーバーに等しいとそれに続くコロンとポート番号。 次に、例を示します。

```console
set _NT_SYMBOL_PROXY=myproxyserver:80
```

この方法で選択した場合、プロキシ サーバーは、SymSrv をシンボル サーバーへのアクセスを使用している任意の Windows デバッガーによって使用されます。 そのシンボル ハンドラーとして DbgHelp を使用するその他のデバッグ ツールによっても使用されます。 この設定では、他のプログラムは影響ありません。

 

 





