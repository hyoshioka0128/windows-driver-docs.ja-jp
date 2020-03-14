---
title: Remote ツールの概念
description: Remote ツールの概念
ms.assetid: 509b25cd-d69a-442d-bd5b-a69266d341c3
keywords:
- リモートツール、リモートツールの概念
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd804aa61f79d37a8879387ad0a8758884302359
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242779"
---
# <a name="remote-tool-concepts"></a>Remote ツールの概念


## <span id="ddk_remote_tool_concepts_dtools"></span><span id="DDK_REMOTE_TOOL_CONCEPTS_DTOOLS"></span>


リモートツールでは、次の概念が使用されます。

### <a name="span-idclient_and_serverspanspan-idclient_and_serverspanclient-and-server"></a><span id="client_and_server"></span><span id="CLIENT_AND_SERVER"></span>クライアントとサーバー

リモートツールでは、*ローカル*および*リモート*という語を回避するクライアントサーバーパラダイムが使用されます。これは、複数のユーザーと複数のコンピューターが存在する場合に混乱を招く可能性がある相対的な用語です。

クライアントコンピューターとサーバーコンピューターに入力したコマンドは、両方のコンピューターのコマンドプロンプトウィンドウに表示されます。

### <a name="span-idthe_serverspanspan-idthe_serverspanthe-server"></a><span id="the_server"></span><span id="THE_SERVER"></span>サーバー

*サーバー*は、コンソールプログラムを実行するコンピューターです。 *リモートサーバー*は、サーバーで実行されているリモートツールのインスタンスです。 サーバーは、リモートセッション (名前付きパイプ) を確立して名前を付け、コンソールプログラムを起動するコマンドを発行して、セッションへの接続が許可されているユーザーを判断します。

### <a name="span-idthe_clientspanspan-idthe_clientspanthe-client"></a><span id="the_client"></span><span id="THE_CLIENT"></span>クライアント

*クライアント*は、コンソールプログラムにコマンドを送信するリモートコンピューターです。 *リモートクライアント*は、クライアントコンピューターで実行されているリモートツールのインスタンスです。 クライアントは、サーバーが確立したリモートセッションに接続し、サーバーが作成したリモートセッション (名前付きパイプ) を使用して、サーバーで実行されているコンソールプログラムにコマンドを送信します。

リモートツールは、各リモートセッションで複数のクライアントをサポートします。 各クライアントは1つのリモートクライアントを実行しています。 すべてのクライアントは、サーバーで実行されているコンソールプログラムにコマンドを送信できます。また、すべてのクライアントは、送信されたコマンドと出力を表示できます。

### <a name="span-idvisible-sessionspanspan-idvisible_sessionspanvisible-session"></a><span id="visible-session"></span><span id="VISIBLE_SESSION"></span>表示可能なセッション

リモートセッションが*表示*されると、コンピューター上のリモートセッションの一覧に表示されます。 一覧を表示するには、[**リモートサーバークエリコマンド**](remote-server-query-command.md)( **/q**) を使用します。

既定では、デバッガーセッションのみが表示されます。つまり、*コマンド*パラメーターの値には、 **kd**、 **dbg**、 **remoteds**、 **ntsd**、または**cdb**という単語が含まれます。それ以外の場合、セッションは表示されません。 *Command*パラメーターは、サーバー上の Remote tool コマンドの一部です。

セッションを表示するには、 **/v**パラメーターを[**リモートサーバー**](remote-server-syntax.md)コマンドに追加します。 デバッガーセッションを非表示にするには、コマンドに **/-v**パラメーターを追加します。

リモートサーバークエリコマンドのヘルプについては、「 [**Remote Server Query command**](remote-server-query-command.md)」を参照してください。

 

 





