---
title: ダイアログ ボックス プロシージャと CPSUI
description: ダイアログ ボックス プロシージャと CPSUI
ms.assetid: fad65a34-9580-41a5-ad58-91ea7ffcd3d5
keywords:
- ページイベントのコールバックの WDK CPSUI
- イベントコールバック WDK CPSUI
- メッセージハンドラー WDK CPSUI
- CPSUI WDK print、メッセージハンドラー
- ダイアログボックスの手順 WDK CPSUI
- ウィンドウメッセージ WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c22be1b6faa75d85dd287e61bd3e9791578c6d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828920"
---
# <a name="dialog-box-procedures-and-cpsui"></a>ダイアログ ボックス プロシージャと CPSUI





ダイアログボックスプロシージャは、システムによって送信されたウィンドウメッセージを処理するコールバック関数です。 CPSUI によって指定されていないカスタマイズされたプロパティシートページを作成する場合は、この種類の[ページイベントコールバック](page-event-callbacks.md)が必要です。 (CPSUI が提供されている[ページとテンプレート](cpsui-supplied-pages-and-templates.md)では、ダイアログボックスプロシージャを使用することもできますが、 [CPSUI メッセージハンドラー](cpsui-message-handler.md)を使用することをお勧めします)。ダイアログボックスの手順の詳細については、Microsoft Windows SDK のドキュメントの「プロパティ」を参照してください。 ダイアログボックスのプロシージャへのポインターは、Windows SDK のドキュメントで説明されている DLGPROC ポインター型を使用して宣言されます。

CPSUI を使用して作成されたすべてのプロパティシートページについて、ウィンドウメッセージは、最初に CPSUI によってインターセプトされてから、アプリケーションで提供されるダイアログボックスのプロシージャに渡されます。 CPSUI が提供するテンプレートを使用してページが定義されている場合、アプリケーションによって提供されるダイアログプロシージャは、CPSUI がメッセージを処理する必要があることを示す戻り値を指定できます。

ダイアログボックスプロシージャでは、 [**setcpsuiuserdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-setcpsuiuserdata)関数と[**getcpsuiuserdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-getcpsuiuserdata)関数を使用して、アプリケーションが提供する値を格納および取得できます。

CPSUI でのダイアログボックスプロシージャの使用の詳細については、「 [**Dlgpage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)」の「解説」を参照してください。

 

 




