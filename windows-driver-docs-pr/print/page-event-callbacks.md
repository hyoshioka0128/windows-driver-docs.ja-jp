---
title: ページ イベント コールバック
description: ページ イベント コールバック
ms.assetid: 891f62ec-d009-42c8-8143-73bfe737a946
keywords:
- WDK CPSUI のコールバック関数
- 共通のプロパティ シートのユーザー インターフェイスの WDK の印刷、コールバック
- CPSUI WDK の印刷、コールバック
- WDK プロパティ シートのページを印刷するコールバック
- ページ イベントのコールバックを WDK CPSUI
- イベントのコールバック WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c262a174865348acecc70f36c614c065aa2731bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574385"
---
# <a name="page-event-callbacks"></a>ページ イベント コールバック





ユーザー プロパティ シート ページが、オペレーティング システムは、フォーカスを変更または変更された値としてこのようなウィンドウのイベントの通知を送信します。 CPSUI アプリケーションがページのウィンドウのイベントの通知を受信する方法は、アプリケーションのページの定義方法によって異なります。

-   使用して、ページが定義された場合、 [CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)を指定できます、 [CPSUI メッセージ ハンドラー](cpsui-message-handler.md)。

-   アプリケーションがない CPSUI によって提供されるカスタマイズされたページを作成する場合は、ダイアログ ボックスのプロシージャを提供します。 詳細については、次を参照してください。 [ ダイアログ ボックス プロシージャと CPSUI](dialog-box-procedures-and-cpsui.md)します。

呼び出すときにページ イベントのコールバックのアドレスを CPSUI CPSUI アプリケーション提供、 [ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)関数。

 

 




