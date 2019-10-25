---
title: CPSUI メッセージ ハンドラー
description: CPSUI メッセージ ハンドラー
ms.assetid: 4a6434e9-d65e-4ddd-836e-d6101532bbb8
keywords:
- ページイベントのコールバックの WDK CPSUI
- イベントコールバック WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb7a806527b3e689a47d8c0b4b3828b316a63d50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831809"
---
# <a name="cpsui-message-handler"></a>CPSUI メッセージ ハンドラー





CPSUI メッセージハンドラーは、 [ **\_CPSUICALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)関数型を使用して定義されたコールバック関数です。 [CPSUI が提供するページとテンプレート](cpsui-supplied-pages-and-templates.md)を使用している場合は、この種類の[ページイベントコールバック](page-event-callbacks.md)をお勧めします。

ユーザーがプロパティシートページを操作してイベントが発生すると、CPSUI はそのイベントをインターセプトし、CPSUICALLBACK 型の関数を \_呼び出して、コールバック関数が実行されている理由を記述する[**Cpsuicbparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam)構造体を提供します。と呼ばれる。

コールバック関数は、イベントを処理し、ページを再表示または再初期化する必要があるかどうかを示す状態値を CPSUI に返す必要があります。

 

 




