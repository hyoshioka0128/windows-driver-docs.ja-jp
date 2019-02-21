---
title: KD 接続サーバー (カーネル モード)
description: KD 接続サーバー (カーネル モード)
ms.assetid: fe0c9110-8fbf-46ae-ae1d-75ab5231aef3
keywords:
- KD 接続サーバー経由のリモート デバッグ
- KD 接続サーバー
- KD 接続サーバー, 概要
- スマート クライアント (カーネル モード)
- KdSrv
- KdSrv, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb2bbe052ff4908935984bcd3b84a14dd5d41d4e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538965"
---
# <a name="kd-connection-servers-kernel-mode"></a>KD 接続サーバー (カーネル モード)


## <span id="ddk_kd_connection_servers_kernel_mode__dbg"></span><span id="DDK_KD_CONNECTION_SERVERS_KERNEL_MODE__DBG"></span>


KD 接続サーバーを介してリモート デバッグをカーネル モードと呼ばれる小規模なアプリケーションを実行している必要があります、 *KD 接続サーバー*サーバー。 クライアントでカーネル モード デバッガーが起動します。 呼び出されたため、このデバッガーは、すべて実際の処理の実行は、*スマート クライアント*します。

Windows のツールをデバッグ パッケージには、KdSrv (kdsrv.exe) と呼ばれる KD 接続のサーバーが含まれています。

2 台のコンピューターを Windows 以外の同じバージョンを実行する必要はありません。任意のバージョンの Windows が実行できます。 ただし、クライアントで使用して、デバッガー バイナリと、サーバーで使用される KdSrv バイナリは、Windows のツールをデバッグ パッケージの同じリリースする必要があります。 このメソッドは、ダンプ ファイルのデバッグに使用できません。

このリモート セッションをセットアップする KD 接続のサーバーは、最初に設定し、スマート クライアントがアクティブ化します。 スマート クライアントの任意の数が 1 つの KD 接続サーバーを通じて動作できますが、各接続するさまざまなカーネルのデバッグ セッションにします。

このセクションの内容:

[KD 接続のサーバーをアクティブ化します。](activating-a-kd-connection-server.md)

[KD 接続のサーバーの検索](searching-for-kd-connection-servers.md)

[スマート クライアント (カーネル モード) をアクティブ化します。](activating-a-smart-client--kernel-mode-.md)

[KD 接続サーバーの例](kd-connection-server-examples.md)

[KD 接続サーバー セッションを制御します。](controlling-a-kd-connection-server-session.md)

 

 





