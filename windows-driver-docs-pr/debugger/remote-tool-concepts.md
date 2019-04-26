---
title: Remote ツールの概念
description: Remote ツールの概念
ms.assetid: 509b25cd-d69a-442d-bd5b-a69266d341c3
keywords:
- リモート ツール、リモート ツールの概念
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd804aa61f79d37a8879387ad0a8758884302359
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353495"
---
# <a name="remote-tool-concepts"></a>Remote ツールの概念


## <span id="ddk_remote_tool_concepts_dtools"></span><span id="DDK_REMOTE_TOOL_CONCEPTS_DTOOLS"></span>


次の概念は、リモート ツールで使用されます。

### <a name="span-idclientandserverspanspan-idclientandserverspanclient-and-server"></a><span id="client_and_server"></span><span id="CLIENT_AND_SERVER"></span>クライアントとサーバー

リモート ツールは、単語を回避するクライアント/サーバー パラダイムを使用して*ローカル*と*リモート*、複数のユーザーと複数のコンピューターがある場合に混乱する相対的な用語であります。

両方のコンピューターのコマンド プロンプト ウィンドウで、クライアントとサーバー コンピューターで入力したコマンドが表示されます。

### <a name="span-idtheserverspanspan-idtheserverspanthe-server"></a><span id="the_server"></span><span id="THE_SERVER"></span>サーバー

*Server*はコンソール プログラムを実行するコンピューターです。 *リモート サーバー*サーバーで実行されているリモート ツールのインスタンスです。 サーバーを確立し、(名前付きパイプ)、リモート セッションの名前を付けます化し、コンソール プログラムを起動するコマンドを発行セッションへの接続が許可されるユーザーを決定します。

### <a name="span-idtheclientspanspan-idtheclientspanthe-client"></a><span id="the_client"></span><span id="THE_CLIENT"></span>クライアント

*クライアント*はコンソール プログラムにコマンドを送信するリモート コンピューターです。 *リモート クライアント*はクライアント コンピューターで実行されているリモート ツールのインスタンスです。 クライアントは、サーバーが設定されたリモート セッションに接続し、サーバー上で実行するコンソール プログラムにコマンドを送信する、サーバーが作成されたリモート セッション (名前付きパイプ) を使用しています。

リモート ツールは、各リモート セッションで複数のクライアントをサポートします。 各クライアントは、1 つのリモート クライアントを実行しています。 すべてのクライアント、サーバーで実行されているコンソール プログラムにコマンドを送信することができ、送信されたコマンドと表示される出力にすべてのクライアントがわかります。

### <a name="span-idvisible-sessionspanspan-idvisiblesessionspanvisible-session"></a><span id="visible-session"></span><span id="VISIBLE_SESSION"></span>表示されているセッション

リモート セッションの場合は*表示*コンピューター上のリモート セッションの一覧に表示されます。 使用して、一覧を表示する、 [**クエリ コマンドをリモート サーバー** ](remote-server-query-command.md) (**/q**)。

既定では、デバッガー セッションのみが表示され、セッションは、の値、*コマンド*パラメーターに含める単語**kd**、 **dbg**、 **remoteds**、 **ntsd**、または**cdb**。 そうしないと、セッションは表示されません。 *コマンド*パラメーターは、サーバーでリモート ツールのコマンドの一部です。

セッションを表示するには、追加、 **/v**パラメーターを[**リモート サーバー** ](remote-server-syntax.md)コマンド。 デバッガー セッションを非表示にするために、追加、 **/v**パラメーターをコマンド。

リモート サーバーのクエリ コマンドのヘルプを参照してください。 [**リモート サーバーのクエリ コマンド**](remote-server-query-command.md)します。

 

 





