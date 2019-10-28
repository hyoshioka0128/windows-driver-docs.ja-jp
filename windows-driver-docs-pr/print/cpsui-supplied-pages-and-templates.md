---
title: CPSUI 指定のページとテンプレート
description: CPSUI 指定のページとテンプレート
ms.assetid: de33cb29-3941-4232-bd61-d36fb04d69d3
keywords:
- 一般的なプロパティシートのユーザーインターフェイス WDK 印刷、テンプレート
- CPSUI WDK print、テンプレート
- プロパティシートページの WDK 印刷、テンプレート
- 共通プロパティシートのユーザーインターフェイス WDK 印刷、定義済みページ
- CPSUI WDK print、事前に定義されたページ
- プロパティシートページ WDK 印刷、定義済みページ
- 事前定義されたプロパティシートページ (WDK CPSUI)
- テンプレート WDK CPSUI
- treeview ページの WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5f869ec3ce350aefcf4d3d160e5cbf9cf999786
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843059"
---
# <a name="cpsui-supplied-pages-and-templates"></a>CPSUI 指定のページとテンプレート





CPSUI は、3つのページテンプレートと共に、定義済みのプロパティシートページのセットを提供します。 定義済みのプロパティシートのページには、次のものがあります。

-   **レイアウト**のタブタイトル、**用紙/品質**、および**高度**な3ページのセット。 これらのページは、プリンターのドキュメントプロパティを格納することを目的としており、プリンターインターフェイス DLL の[**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)関数内からプロパティシートを作成するために使用できます。

-   タブタイトルが **[詳細**] の単一ページ。 ここでも、このページはプリンターのドキュメントプロパティを格納することを意図しており、プリンターインターフェイス DLL の[**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)関数内からプロパティシートを作成するために使用できます。

-   **デバイス設定**のタブタイトルを持つ単一のページ。 このページは、プリンターのプロパティを格納するためのものであり、プリンターインターフェイス DLL の[**DrvDevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)関数内からプロパティシートを作成するために使用できます。

-   定義済みのタイトルのない単一の汎用 treeview ページ。 CPSUI アプリケーションでは、このページを使用できます。

定義済みページを使用するには、アプリケーションで、 [**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)構造体の**pDlgPage**メンバーを使用して識別する必要があります。

CPSUI には、3つの定義済みページテンプレートも用意されています。 CPSUI は、これらのテンプレートを使用して、定義済みページを作成します。 また、アプリケーションで使用することもできます。 テンプレートは、次の要素で構成されています。

-   Treeview ページテンプレート。 CPSUI は、定義済みの **[詳細**設定] ページと **[デバイスの設定]** ページを作成するために使用します。 このテンプレートは、各[プロパティシートオプション](property-sheet-options.md)のノードを含む treeview コントロールで構成されています。 コンテキストメニューは、ツリーの各ノードに関連付けられています。 各ノードのコンテキストメニューには、ユーザーがオプションの値を変更するための手段が用意されています。 CPSUI は、 [CPSUI でサポートされているすべてのウィンドウコントロール](cpsui-supported-window-controls.md)の Windows メッセージを処理する、このテンプレートのダイアログボックスプロシージャを提供します。

-   2つの複数のコントロールテンプレート。 CPSUI を使用して、定義済みの**レイアウト**と**用紙/品質**のページを作成します。 CPSUI は、CPSUI でサポートされているすべてのウィンドウコントロールの Windows メッセージを処理する、このテンプレートのダイアログボックスプロシージャを提供します。

定義済みのページテンプレートを使用するには、アプリケーションで、 [**dlgpage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)構造体の**DlgTemplateID**メンバーを使用して識別する必要があります。

 

 




