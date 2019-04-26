---
title: トレース セッションの停止
description: トレース セッションの停止
ms.assetid: 648bf805-4266-4db5-aef6-414c5f37d1a3
keywords:
- トレース セッションを停止する WDK
- トレース セッションを停止しています
- Traceview で WDK、トレースを停止します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2dc5a0671cb01c676c8d4afd74d6d8b80c94cae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345784"
---
# <a name="stopping-a-trace-session"></a>トレース セッションの停止


ときにする*停止*traceview で無効にします。 トレース プロバイダーでは、トレース セッションは、すべての未送信のトレース メッセージをバッファーから、traceview で表示し、トレース ログ、および、トレース セッションを停止しますにフラッシュします。 トレース セッションを停止するには、次の操作を行います。

1.  [トレース セッション リスト](trace-session-list.md)、トレース セッションで、行の任意のセルを右クリックします。

2.  クリックして**トレースを停止**します。

値を簡単な一時停止した後、**状態**から変更する列**を実行している**に**停止**し**停止**します。 ときに、トレース セッションが停止すると、[表示から削除](removing-a-trace-session.md)します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview では、起動してトレース セッションのみを停止できます。 他のトレース セッションを停止する、**traceview で-停止 * * * SessionName*コマンド。 このコマンドの詳細については、次を参照してください。 [ **traceview で管理コマンド**](traceview-control-commands.md)します。

トレース セッションを停止する、表示から、セッションを削除したりしないすべてのトレース ログを削除します。

Traceview でを使用して、 **EnableTrace**トレース セッションを停止する関数。 この関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





