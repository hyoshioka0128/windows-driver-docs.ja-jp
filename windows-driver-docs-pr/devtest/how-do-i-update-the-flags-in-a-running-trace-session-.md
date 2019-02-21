---
title: 実行中のトレース セッションで、フラグを更新する方法
description: 実行中のトレース セッションで、フラグを更新する方法
ms.assetid: 952cc60f-1877-49d5-b87c-493c1b90cfdf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 467431b21c66864d5dcf018704c030acdf30473b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536659"
---
# <a name="how-do-i-update-the-flags-in-a-running-trace-session"></a>実行中のトレース セッションで、フラグを更新する方法


変更する、[トレース フラグ](trace-flags.md)または[トレース レベル](trace-level.md)実行中のトレース セッションで使用して、 **tracelog-有効にする**コマンドが、 **tracelog-を更新**コマンド。 詳細については、次を参照してください。 [ **Tracelog コマンド構文**](tracelog-command-syntax.md)します。

フラグとレベルのプロパティを[トレース プロバイダー](trace-provider.md)のではありません、[トレース セッション](trace-session.md)します。 そのため、 **tracelog-更新**、トレース セッションを更新するコマンドを使用してプロバイダーのプロパティを変更することはできません。 代わりに、使用、 **tracelog-有効にする**新しいプロパティを使用してプロバイダーを再度有効にするコマンド。

については、 **tracelog-有効にする**コマンドを参照してください[ **Tracelog コマンド構文**](tracelog-command-syntax.md)します。 このコマンドを使用する方法の例は、次を参照してください。[例 5。トレース プロバイダーを有効にする](example-5--enabling-trace-providers.md)します。

使用することも[traceview で](traceview.md)traceview でを使用して開始したトレース セッションで、フラグまたはレベルを変更します。 グラフィカル ユーザー インターフェイスはそれらを変更して、セッションの実行中にどのようなプロパティを表示する簡単に変更できます。

 

 





