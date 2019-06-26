---
title: 新しいプロパティ シートのページを追加する
description: 新しいプロパティ シートのページを追加する
ms.assetid: ec4303e9-889c-41ee-8872-ddefdc906eb2
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、プロパティ シート ページ
- UI プラグインを WDK の印刷、プロパティ シートのページ
- WDK プロパティ シートのページを印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e0fd82cc541294ed69ea723c280fee1ceb34ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370501"
---
# <a name="adding-new-property-sheet-pages"></a>新しいプロパティ シートのページを追加する





新しいページを Unidrv または Pscript5、プラグイン UI プリンター インターフェイスによって提供されるプロパティ シートを追加する場合は、次の IPrintOemUI メソッドを実装する必要があります。

-   [**IPrintOemUI::DevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)

    ユーザーが選択したときに表示されるプリンターのプロパティ シートに追加するために使用、**プロパティ**プリンター フォルダーまたはプリンターのウィンドウから、または、アプリケーションが PrinterProperties 関数を呼び出すときにメニュー項目 (で説明されている、Windows SDK ドキュメント)。

-   [**IPrintOemUI::DocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)

    ユーザーが選択したときに表示されるドキュメントのプロパティ シートにページを追加するために使用、**プリンターの設定**プリンター フォルダーまたはプリンターのウィンドウから、またはアプリケーションを呼び出すと、DocumentProperties メニュー項目または(Windows SDK のドキュメントで説明した) AdvancedDocumentProperties 関数。

これらのメソッドを実装する場合は通常も指定する、 [  **\_CPSUICALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-_cpsuicallback)-ユーザーによる変更を処理するコールバック関数を入力します。 このコールバック関数を呼び出す必要があります[ **IPrintOemDriverUI::DrvUpdateUISetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)設定の値がある場合、ユーザー インターフェイスの設定に関連付けられた値が変更されたときに、ドライバーに通知するにはドライバーに格納されている[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体またはレジストリのキー。

 

 




