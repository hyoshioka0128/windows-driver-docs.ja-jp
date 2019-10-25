---
title: ページ イベント コールバック
description: ページ イベント コールバック
ms.assetid: 891f62ec-d009-42c8-8143-73bfe737a946
keywords:
- コールバック関数 WDK CPSUI
- 共通プロパティシートのユーザーインターフェイス WDK print、コールバック
- CPSUI WDK print、コールバック
- プロパティシートページの WDK 印刷、コールバック
- ページイベントのコールバックの WDK CPSUI
- イベントコールバック WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a440a4f5ee9910ae982304c6739447fffcf4f4c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845048"
---
# <a name="page-event-callbacks"></a>ページ イベント コールバック





ユーザーがプロパティシートページを操作すると、操作システムは、変更されたフォーカスまたは変更された値としてそのようなウィンドウイベントの通知を送信します。 CPSUI アプリケーションがページのウィンドウイベントの通知を受信する方法は、アプリケーションでページがどのように定義されているかによって異なります。

-   [CPSUI が提供するページとテンプレート](cpsui-supplied-pages-and-templates.md)を使用してページが定義されている場合は、 [CPSUI メッセージハンドラー](cpsui-message-handler.md)を指定できます。

-   CPSUI で提供されていないカスタマイズされたページをアプリケーションで作成した場合は、ダイアログボックスの手順を提供する必要があります。 詳細については、「[ダイアログボックスのプロシージャと CPSUI](dialog-box-procedures-and-cpsui.md)」を参照してください。

CPSUI アプリケーションは、 [**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)関数を呼び出すときに、ページイベントコールバックのアドレスを CPSUI に提供します。

 

 




