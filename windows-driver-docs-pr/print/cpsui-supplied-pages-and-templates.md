---
title: CPSUI 指定のページとテンプレート
description: CPSUI 指定のページとテンプレート
ms.assetid: de33cb29-3941-4232-bd61-d36fb04d69d3
keywords:
- 共通のプロパティ シートのユーザー インターフェイスの WDK、印刷テンプレート
- CPSUI WDK、印刷テンプレート
- WDK のプロパティ シート ページが印刷テンプレート
- 共通のプロパティ シートのユーザー インターフェイスの WDK 印刷、定義済みのページ
- 定義済みページの印刷、CPSUI WDK
- WDK プロパティ シートのページを印刷する定義済みページ
- 定義済みのプロパティ シート ページ WDK CPSUI
- WDK CPSUI テンプレート
- treeview は、WDK CPSUI をページします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 937d7192ced24d4bd33c22a52f37868197ea9536
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372449"
---
# <a name="cpsui-supplied-pages-and-templates"></a>CPSUI 指定のページとテンプレート





CPSUI には、次の 3 つのページ テンプレートと共に、定義済みのプロパティ シートのページのセットが用意されています。 定義済みのプロパティ シートのページを以下に示します。

-   一連の 3 つのページのタブのタイトルと**レイアウト**、**用紙/品質**、および**詳細**します。 これらのページは、プリンターのドキュメント プロパティが含まれるものし、プリンターのインターフェイス内で DLL からプロパティ シートを作成するために使用できます[ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)関数。

-   タブのタイトルと、1 つのページ**詳細**します。 ページのプリンターなどのドキュメント プロパティを格納するためのものが、もう一度とプリンターのインターフェイス内で DLL からプロパティ シートを作成するために使用できます[ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)関数。

-   タブのタイトルと、1 つのページ**デバイス設定**します。 このページは、プリンターのプロパティが含まれるものでは、プリンターのインターフェイス内で DLL からプロパティ シートを作成するために使用できる[ **DrvDevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets)関数。

-   定義済みのタイトルなしで 1 つの一般的なツリー ビュー ページ。 任意の CPSUI アプリケーションには、このページを使用できます。

定義済みのページを使用するアプリケーション特定する必要がありますを使用して、 **pDlgPage**のメンバー、 [ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)構造体。

CPSUI には、次の 3 つの定義済みページ テンプレートも用意されています。 CPSUI は、その定義済みのページを作成するため、これらのテンプレートを使用します。 アプリケーションはそれらも使用できます。 次のテンプレートが構成されます。

-   CPSUI は定義済みの作成を使用して treeview ページのテンプレート**詳細**と**デバイス設定**ページ。 このテンプレートは各ノードを格納する treeview コントロールの構成[プロパティ シート オプション](property-sheet-options.md)します。 コンテキスト メニューは、ツリーの各ノードに関連付けられます。 各ノードのコンテキスト メニューは、ユーザーがオプションの値を変更する手段を提供します。 CPSUI このテンプレートは、すべての Windows メッセージを処理するためのダイアログ ボックス プロシージャを提供する、 [CPSUI でサポートされているウィンドウ コントロール](cpsui-supported-window-controls.md)します。

-   2 つ CPSUI は定義済みの作成を使用して複数のコントロール テンプレート、**レイアウト**と**用紙/品質**ページ。 CPSUI には、このテンプレートでは、すべてのウィンドウの CPSUI でサポートされているコントロールの Windows メッセージを処理のダイアログ ボックス プロシージャが用意されています。

定義済みのページのテンプレートを使用するアプリケーション特定する必要がありますを使用して、 **DlgTemplateID**のメンバー、 [ **DLGPAGE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_dlgpage)構造体。

 

 




