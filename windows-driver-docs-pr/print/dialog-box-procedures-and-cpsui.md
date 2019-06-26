---
title: ダイアログ ボックス プロシージャと CPSUI
description: ダイアログ ボックス プロシージャと CPSUI
ms.assetid: fad65a34-9580-41a5-ad58-91ea7ffcd3d5
keywords:
- ページ イベントのコールバックを WDK CPSUI
- イベントのコールバック WDK CPSUI
- メッセージ ハンドラー WDK CPSUI
- CPSUI WDK 印刷、メッセージ ハンドラー
- ダイアログ ボックス プロシージャ WDK CPSUI
- ウィンドウ メッセージを WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b50d323ebdec809f5e033437634561f8514dc2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360210"
---
# <a name="dialog-box-procedures-and-cpsui"></a>ダイアログ ボックス プロシージャと CPSUI





ダイアログ ボックス プロシージャは、システムによって送信されたウィンドウ メッセージを処理するコールバック関数です。 この種類の[ページ イベント コールバック](page-event-callbacks.md)CPSUI では提供されないカスタマイズされたプロパティ シート ページを作成する場合は必須です。 (を使用したダイアログ ボックス プロシージャを使用することもできます[CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)、の使用が、 [CPSUI メッセージ ハンドラー](cpsui-message-handler.md)をお勧めします。)。ダイアログ ボックス プロシージャの詳細については、Microsoft Windows SDK ドキュメントの DialogProc を参照してください。 ダイアログ ボックス プロシージャへのポインターは、Windows SDK ドキュメントの説明も DLGPROC ポインター型を使用して宣言されます。

CPSUI を使用して作成されたすべてのプロパティ シート ページ、ウィンドウ メッセージ最初によって傍受される CPSUI、アプリケーションによって提供されるダイアログ ボックス プロシージャに渡される前にします。 CPSUI が指定したテンプレートを使用して、ページの定義 ダイアログのアプリケーションによって提供されるプロシージャは CPSUI がメッセージを処理することを示す戻り値を指定できます。

ダイアログ ボックスのプロシージャを使用できます、 [ **SetCPSUIUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-setcpsuiuserdata)と[ **GetCPSUIUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-getcpsuiuserdata)関数を格納および取得します。アプリケーションによって提供される値。

CPSUI でダイアログ ボックス プロシージャの使用に関する詳細については、「解説」を参照してください。 [ **DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage)します。

 

 




