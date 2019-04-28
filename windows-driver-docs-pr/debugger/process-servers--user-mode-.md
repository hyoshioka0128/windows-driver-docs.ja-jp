---
title: プロセス サーバー (ユーザー モード)
description: プロセス サーバー (ユーザー モード)
ms.assetid: 9391fcd4-c64f-4c2b-89c2-da09be7646d1
keywords:
- プロセス サーバーをリモート デバッグ
- プロセス サーバー
- プロセス サーバー、概要
- スマート クライアント (ユーザー モード)
- DbgSrv
- DbgSrv, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 169761324cce07939590b34ec0e1421d5377b02d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362405"
---
# <a name="process-servers-user-mode"></a>プロセス サーバー (ユーザー モード)


## <span id="ddk_process_servers_user_mode__dbg"></span><span id="DDK_PROCESS_SERVERS_USER_MODE__DBG"></span>


プロセス サーバーをリモート デバッグと呼ばれる小規模なアプリケーションを実行している必要があります、*プロセス サーバー*サーバー コンピューターにします。 クライアント コンピューターのユーザー モード デバッガーが起動します。 呼び出されたため、このデバッガーは、すべて実際の処理の実行は、*スマート クライアント*します。

Windows のツールをデバッグ パッケージには、ユーザー モードで使用するための DbgSrv (dbgsrv.exe) と呼ばれるプロセス サーバーが含まれています。

2 台のコンピューターを Windows 以外の同じバージョンを実行する必要はありません。任意のバージョンの Windows が実行できます。 ただし、クライアントで使用して、デバッガー バイナリと、サーバーで使用される DbgSrv バイナリは、Windows のツールをデバッグ パッケージの同じリリースする必要があります。 このメソッドは、ダンプ ファイルのデバッグに使用できません。

このリモート セッションをセットアップするプロセス サーバーは、最初に設定し、スマート クライアントがアクティブ化します。 スマート クライアントの任意の数が 1 つのプロセス サーバーを通じて動作できる - これらのデバッグ セッションは独立したままになりは互いに影響しません。 実行するプロセス サーバーは引き続きデバッグ セッションが終了した場合の新しいデバッグ セッションで使用します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [**プロセス サーバーをアクティブ化します。**](activating-a-process-server.md)
-   [**プロセス サーバーの検索**](searching-for-process-servers.md)
-   [**スマート クライアントのアクティブ化**](activating-a-smart-client.md)
-   [プロセス サーバーの例](process-server-examples.md)
-   [プロセス サーバーのセッションを制御します。](controlling-a-process-server-session.md)

 

 





