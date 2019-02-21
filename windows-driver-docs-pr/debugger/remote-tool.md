---
title: リモート ツール
description: リモート ツール、Remote.exe は、コマンド ライン ツールを実行し、リモート コンピューターのコンソール プログラムを制御することができます。
ms.assetid: b6fbde9b-1a2a-46b8-9edc-7fa143f5a711
keywords:
- リモート ツール
- Remote.exe
- Remote.exe、リモート ツールを参照してください。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6859127b5d6f86606161440495c73ac2d0b756f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551987"
---
# <a name="remote-tool"></a>リモート ツール


リモート ツール、Remote.exe は、コマンド ライン ツールを実行し、リモート コンピューターのコンソール プログラムを制御することができます。

## <a name="span-idwheretogettheremotetoolspanspan-idwheretogettheremotetoolspanspan-idwheretogettheremotetoolspanwhere-to-get-the-remote-tool"></a><span id="Where_to_get_the_Remote_tool"></span><span id="where_to_get_the_remote_tool"></span><span id="WHERE_TO_GET_THE_REMOTE_TOOL"></span>リモート ツールの入手先


含まれている Remote.exe[ツールを Windows のデバッグ](index.md)します。

## <a name="span-idddkremotetooldtoolsspanspan-idddkremotetooldtoolsspanremote-tool-components"></a><span id="ddk_remote_tool_dtools"></span><span id="DDK_REMOTE_TOOL_DTOOLS"></span>リモート ツールのコンポーネント


リモート ツールには、次のコンポーネントが含まれています。

-   サーバー アプリケーション コンソール プログラムを起動し、クライアント接続の名前付きパイプに開きますです。

-   サーバーへの接続を確立するクライアント アプリケーションです。 クライアント コンピューターに型指定されたコマンドがサーバーで、コンソール アプリケーションに送信し、リモート クライアントがサーバーのコンソール ウィンドウからの出力を表示します。

-   サーバー コンピューターで実行されているリモート セッションの一覧をクエリする機能。

リモート ツールを 1 台のコンピューターが複数のクライアントは、各セッションに接続できます複数サーバーのセッションを開始できます。 セッションは、コンピューターのリソースによってのみ制限されます。

これより高度なツール、リモート デスクトップを主に譲りますされましたが、以前のツールです。 ただし、ので、簡単ですし、わずかなリソースを使用してがも引き続き広く使用が、通常のリモート デバッグします。

リモート ツールは、ローカルおよびリモートの両方のコンピューターでコマンドを送信することが必要です。 そのため、ローカル ユーザーのないコンピューターでこのツールを使用するには、コマンドを送信して、必要に応じて、コンピューターの再起動を別の方法を開発する必要があります。

リモート ツールは、ユーザーを認証したり、Microsoft Windows のアクセス許可を使用しないため、コンピューターには、セキュリティを損なうことができます。 既定では、接続およびセッションの名前を指定できる任意のリモート コンピューターを特定のユーザーとグループを含めたり除外したり、リモート ツールのオプションを使用できますが、このツールを作成する名前付きパイプを使用できます。

このセクションの内容:

[リモート ツールの概念](remote-tool-concepts.md)

[リモート ツールのコマンド](remote-tool-commands.md)

[リモート ツールの例](remote-tool-examples.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows 用デバッグ ツールに含まれるツール](extra-tools.md)

 

 






