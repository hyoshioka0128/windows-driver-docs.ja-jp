---
title: 新しいプロパティ シートのページを追加する
description: 新しいプロパティ シートのページを追加する
ms.assetid: ec4303e9-889c-41ee-8872-ddefdc906eb2
keywords:
- ユーザーインターフェイスプラグイン WDK print、プロパティシートページ
- UI プラグイン WDK print、プロパティシートページ
- プロパティシートページの WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e14ef057b94ec7d0ffdb43064c635b40f60a805
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843264"
---
# <a name="adding-new-property-sheet-pages"></a>新しいプロパティ シートのページを追加する





プリンターインターフェイスによって Unidrv または Pscript5 に提供されるプロパティシートに新しいページを追加する場合、UI プラグインは次の IPrintOemUI メソッドを実装する必要があります。

-   [**IPrintOemUI::D evicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)

    プリンタープロパティシートに追加するために使用します。これは、ユーザーがプリンターフォルダーまたはプリンターウィンドウから **[プロパティ]** メニュー項目を選択したとき、またはアプリケーションがプリンターのプロパティ機能を呼び出したときに表示されます (Windows SDK のドキュメントを参照).

-   [**IPrintOemUI::D ocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)

    ドキュメントプロパティシートにページを追加するために使用します。これは、ユーザーがプリンターフォルダーまたはプリンターウィンドウから **[プリンターの設定]** メニュー項目を選択したとき、またはアプリケーションが DocumentProperties または AdvancedDocumentProperties を呼び出したときに表示されます。関数 (Windows SDK のドキュメントを参照)。

これらのメソッドのいずれかを実装する場合は、通常、ユーザーの変更を処理するための[ **\_CPSUICALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)型のコールバック関数も指定します。 このコールバック関数は[**Iprintoemdriverui::D rvupdateuisetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)を呼び出して、ユーザーインターフェイス設定に関連付けられた値が変更されたときにドライバーに通知する必要があります (設定の値がドライバーの[**devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体に格納されている場合)。レジストリキー。

 

 




