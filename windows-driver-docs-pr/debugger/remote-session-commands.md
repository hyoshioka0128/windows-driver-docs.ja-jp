---
title: リモート セッションのコマンド
description: リモート セッションのコマンド
ms.assetid: 8c7da3e9-c983-4253-92fb-ce64f22cdc6c
keywords:
- リモート ツールで、コマンドをリモート セッション
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16cb7320d235c7a7ad2b2731d5ec65fa8a902f13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530924"
---
# <a name="remote-session-commands"></a>リモート セッションのコマンド


## <span id="ddk_remote_session_commands_dtools"></span><span id="DDK_REMOTE_SESSION_COMMANDS_DTOOLS"></span>


コンソール セッション中に、リモート ツールとの通信には、次のコマンドを使用します。

<span id="_H"></span><span id="_h"></span><strong>@H</strong>  
サーバーとクライアント コンピューターでセッションのコマンドを表示します。 サーバーとクライアント コンピューターで動作します。

<span id="_M_Message"></span><span id="_m_message"></span><span id="_M_MESSAGE"></span><strong>@M</strong> *メッセージ*  
すべてのサーバーとクライアント コンピューターで、セッションで指定されたメッセージを表示します。 サーバーとクライアント コンピューターで動作します。

<span id="_P_Message"></span><span id="_p_message"></span><span id="_P_MESSAGE"></span><strong>@P</strong> *メッセージ*  
指定したメッセージ サーバー コンピューターのポップアップ ウィンドウを生成します。 クライアント コンピューターでは、コマンド ウィンドウで、メッセージが表示されます。 サーバーとクライアント コンピューターで動作します。

<span id="_Q"></span><span id="_q"></span><strong>@Q</strong>  
終了します。 クライアント コンピューターは、セッションから切断します。 クライアント コンピューターでのみ動作します。

<span id="_K"></span><span id="_k"></span><strong>@K</strong>  
すべてのクライアントを切断し、リモート セッションを終了します。 サーバー コンピューターでのみ動作します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

サンプルについては、「the セッション コマンドを使用して」を参照してください[リモート ツール例](remote-tool-examples.md)します。

セッションのコマンドに応答して、リモート ツールは、コマンドを実行した日時を持つラベルを表示します。 サーバー コンピューターのタイム ゾーンでは、すべてのイベントの時刻が表示されます。

 

 





