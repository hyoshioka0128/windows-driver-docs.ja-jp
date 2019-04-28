---
title: CPSUI メッセージ ハンドラー
description: CPSUI メッセージ ハンドラー
ms.assetid: 4a6434e9-d65e-4ddd-836e-d6101532bbb8
keywords:
- ページ イベントのコールバックを WDK CPSUI
- イベントのコールバック WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7412023503beac133b921d08a502cf8934ae2ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365576"
---
# <a name="cpsui-message-handler"></a>CPSUI メッセージ ハンドラー





CPSUI メッセージ ハンドラーは、コールバック関数を使用して定義されている、 [  **\_CPSUICALLBACK** ](https://msdn.microsoft.com/library/windows/hardware/ff564313)関数の型。 この種類の[ページ イベント コールバック](page-event-callbacks.md)使用するかどうかは推奨[CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)します。

CPSUI はイベントと呼び出しをインターセプトときに、ユーザーは、プロパティ シートのページと対話し、により発生するイベントを\_CPSUICALLBACK に型指定された関数を指定して、 [ **CPSUICBPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff547088)理由のコールバック関数を記述する構造体が呼び出されています。

コールバック関数は、イベントを処理し、ページが再表示または再初期化する必要があるかどうかを示す CPSUI にステータス値を返す必要があります。

 

 




