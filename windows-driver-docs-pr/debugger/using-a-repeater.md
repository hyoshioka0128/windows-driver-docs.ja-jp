---
title: repeater の使用
description: repeater の使用
ms.assetid: c6904b6d-f28b-4494-95d0-9e6fc3dc10f3
keywords:
- repeater、repeater を使用します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bd5f3757abab3dcbfeb266cb73749107ecf4c18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367970"
---
# <a name="using-a-repeater"></a>repeater の使用


## <span id="ddk_using_a_repeater_dbg"></span><span id="DDK_USING_A_REPEATER_DBG"></span>


Repeater 接続は、非常に単純なルールに従います。

-   サーバーとクライアントが互いの予定のすべての通信は、変更を加えることがなく repeater を通過します。

-   サーバーがトランスポート接続に対して実行するアクションは、repeater に影響を与えます (および、クライアントを直接のみに影響)。

-   トランスポート接続に関して、クライアントを実行するアクションは、repeater に影響を与えます (および、サーバーにのみ直接影響しない)。

つまり、任意のデバッグ コマンドをデバッガーの出力コントロール キー、およびファイルへのアクセスが行われる、クライアントとサーバーが直接接続されている場合とまったく同様です。 Repeater はこれらすべてのコマンドに表示されません。

アクション自体の接続を終了するには、repeater に影響します。 たとえば、発行した場合、 [ **qq (終了)** ](q--qq--quit-.md)サーバーがシャット ダウンとトランスポートにシャット ダウンの通知を送信、クライアントからのコマンドします。 これにより、終了する中継ぎ局 (起動時に使用された場合を除き、 **-p**オプション)。 別の例として、 [ **.clients (デバッグ クライアントを一覧表示)** ](-clients--list-debugging-clients-.md)コマンドは、クライアントのコンピューター名では、ボックスの一覧が、repeater で、サーバーに接続するために使用する接続プロトコルが表示されます。

リピータが自動的に終了されている場合は、サーバーがシャット ダウン (起動時に使用された場合を除き、 **-p**オプション)。 リピータ シャット ダウン時、スマート クライアントはありませんが、同様に、終了するデバッグのクライアントがこれにより。 何らかの理由は、直接、repeater を終了する必要が場合は、タスク マネージャーまたは kill.exe ツールを使用できます。

 

 





