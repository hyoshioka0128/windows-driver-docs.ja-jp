---
title: リモート サーバーのクエリ コマンド
description: ローカル コンピューターまたはリモート サーバーで利用可能なセッションの一覧を表示するには、次の構文を使用します。
ms.assetid: c95114a3-2ff5-456b-90e2-4d7bc6346f1f
keywords:
- リモート サーバーのクエリ コマンドの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Remote Server Query Command
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d98ff180d451e52e4f2e4e2b11b3c1240d95d37c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549014"
---
# <a name="remote-server-query-command"></a>リモート サーバーのクエリ コマンド


ローカル コンピューターまたはリモート サーバーで利用可能なセッションの一覧を表示するには、次の構文を使用します。

```console
remote /q Computer
```dbgcmd

## <span id="ddk_remote_server_query_command_dtools"></span><span id="DDK_REMOTE_SERVER_QUERY_COMMAND_DTOOLS"></span>Parameters


<span id="________q______"></span><span id="________Q______"></span> **/q**   
Query. Displays the visible remote sessions on the specified computer.

<span id="_______Computer______"></span><span id="_______computer______"></span><span id="_______COMPUTER______"></span> *Computer*   
Specifies the name of the computer. This parameter is required (even on the local computer).

### <span id="comments"></span><span id="COMMENTS"></span>Comments

The query display includes only server sessions; it does not display client connections to remote sessions.

The query display includes only visible sessions. There is no command to display invisible sessions.

The query display includes all visible sessions, including those that restrict users (**/u** and **/ud**). The user might not have permission to connect to all of the sessions in the list.

When there are no remote sessions running on the server, the Remote tool displays the following message:

```console
No Remote servers running on \\Computer
```

ただし、コンピューターで実行されているのみのリモート セッションが非表示のリモート セッションの場合は、リモート ツールには、次のメッセージが表示されます。

```console
No visible sessions on server \\Computer
```

 

 





