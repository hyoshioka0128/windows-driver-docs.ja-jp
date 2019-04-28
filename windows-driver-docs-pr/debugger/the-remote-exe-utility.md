---
title: Remote.exe ユーティリティ
description: Remote.exe ユーティリティ
ms.assetid: 3780d632-939e-4adb-82f1-fd7c25706b54
keywords:
- remote.exe、remote.exe ユーティリティを使用して、リモート デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc26101fbe58a0d1d95abc0fd9801e1666d7a21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365985"
---
# <a name="the-remoteexe-utility"></a>Remote.exe ユーティリティ


## <span id="ddk_the_remote_exe_utility_dbg"></span><span id="DDK_THE_REMOTE_EXE_UTILITY_DBG"></span>


Remote.exe ユーティリティは、リモート コンピューターでコマンド ライン プログラムを実行できる汎用性の高いサーバー/クライアント ツールです。

Remote.exe では、入力と出力の STDIN および STDOUT を使用するアプリケーションに名前付きパイプを使用してリモート ネットワーク アクセスを提供します。 ネットワークでは、他のコンピューターのユーザーまたはダイヤルアップ モデム接続で接続します。 リモート セッションを表示するか自身のコマンドを入力します。

このユーティリティには、多数の用途があります。 たとえば、ソフトウェアを開発しているときにコンピューターに他のタスクの実行中にプロセッサおよびリモート コンピューターのリソースを使用したコードをコンパイルできます。 特定のタスクの処理要件を複数のコンピューターに分散させる remote.exe を使用することもできます。

その remote.exe、セキュリティ上の承認は行われません、Remote.exe サーバーへの接続に Remote.exe クライアントを実行するすべてのユーザーに許可することを注意してください。 これにより、Remote.exe サーバーが実行されるオープンに接続するすべてのユーザー アカウントです。

 

 





