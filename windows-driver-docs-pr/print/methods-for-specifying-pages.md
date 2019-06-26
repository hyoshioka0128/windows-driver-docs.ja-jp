---
title: ページを指定するためのメソッド
description: ページを指定するためのメソッド
ms.assetid: 76006a2b-37b9-4490-913e-dcfc01812d43
keywords:
- 共通のプロパティ シートのユーザー インターフェイスを WDK を印刷するページの指定
- CPSUI WDK を印刷するページの指定
- WDK のプロパティ シート ページが印刷を指定します。
- COMPROPSHEETUI
- PROPSHEETPAGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8ee69c614031a743cae0d2a24a3e17b8b9bc87b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353510"
---
# <a name="methods-for-specifying-pages"></a>ページを指定するためのメソッド





アプリケーションでは 3 つのメソッドを使用 CPSUI にプロパティ シートのページを指定するのにことができます。 CPSUI の呼び出しでは、次のメソッドの各[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)のいずれかを指定する、関数、 [ComPropSheet 関数コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)します。

-   指定する、 [ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)構造体

    COMPROPSHEETUI 構造体を渡すことによって、アプリケーションがプロパティ シート ページをについて説明するかどうか**ComPropSheet**、そのことができます。

    -   いずれかを使用して、 [CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)、定義済みの標準的なページは、そのプリンターを入力するかを指定するインターフェイスの Dll がプリンターのプロパティ シートを使用できます。
    -   一連のユーザーが変更可能な指定[プロパティ シート オプション](property-sheet-options.md)ページに表示されます。
    -   指定、[ページ イベント コールバック](page-event-callbacks.md)関数 CPSUI を呼び出すときに、ユーザーを表示またはページのオプションを変更します。
-   PROPSHEETPAGE 構造体を指定します。

    COMPROPSHEETUI 構造体を使用する場合に使用できる一般的な (標準) ダイアログ ボックスを使用して、ページを構築できない場合、プロパティ シート ページを記述する (Microsoft Windows SDK のドキュメントで説明) PROPSHEETPAGE 構造体を使用できます。 プリンターのインターフェイスの Dll は、通常、このメソッドを使用するは必要ありません。

-   コールバック関数を指定します。

    アプリケーションに渡すことができます[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)のアドレスを[ **PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfnpropsheetui)-コールバック関数では、どの CPSUI をすぐに型指定されました。呼び出されます。 コールバック関数が呼び出し元の責任**ComPropSheet**自体と、プロパティ シートのページを作成します。

    印刷スプーラをプリンター インターフェイス DLL の CPSUI の存在を通知するためにこのメソッドを使用して**DrvDocumentPropertySheets**と*Pscript*ドライバー CPSUIの存在を通知するために、この手法を使用して[**IPrintOemUI::DocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)と[ **IPrintOemUI::DevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)内の COM メソッド[ユーザープラグインのインターフェイス](user-interface-plug-ins.md)します。

新しいページを指定する方法のいずれかを使用すると、ページ割り当てる必要があります、[グループの親](group-parent.md)へのハンドルの親グループに渡すことによって、 **ComPropSheet**関数。

 

 




