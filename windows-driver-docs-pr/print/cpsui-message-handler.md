---
title: CPSUI メッセージ ハンドラー
description: CPSUI メッセージ ハンドラー
ms.assetid: 4a6434e9-d65e-4ddd-836e-d6101532bbb8
keywords:
- ページ イベントのコールバックを WDK CPSUI
- イベントのコールバック WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82338185b587b89432686b1f3c0bd28891f2055e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372456"
---
# <a name="cpsui-message-handler"></a>CPSUI メッセージ ハンドラー





CPSUI メッセージ ハンドラーは、コールバック関数を使用して定義されている、 [  **\_CPSUICALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback)関数の型。 この種類の[ページ イベント コールバック](page-event-callbacks.md)使用するかどうかは推奨[CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)します。

CPSUI はイベントと呼び出しをインターセプトときに、ユーザーは、プロパティ シートのページと対話し、により発生するイベントを\_CPSUICALLBACK に型指定された関数を指定して、 [ **CPSUICBPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_cpsuicbparam)理由のコールバック関数を記述する構造体が呼び出されています。

コールバック関数は、イベントを処理し、ページが再表示または再初期化する必要があるかどうかを示す CPSUI にステータス値を返す必要があります。

 

 




