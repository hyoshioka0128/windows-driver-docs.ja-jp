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
ms.openlocfilehash: 3267ce97f51253b7c18b1c09417c2e6c77be1187
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358606"
---
# <a name="methods-for-specifying-pages"></a>ページを指定するためのメソッド





アプリケーションでは 3 つのメソッドを使用 CPSUI にプロパティ シートのページを指定するのにことができます。 CPSUI の呼び出しでは、次のメソッドの各[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)のいずれかを指定する、関数、 [ComPropSheet 関数コード](https://msdn.microsoft.com/library/windows/hardware/ff546214)します。

-   指定する、 [ **COMPROPSHEETUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546211)構造体

    COMPROPSHEETUI 構造体を渡すことによって、アプリケーションがプロパティ シート ページをについて説明するかどうか**ComPropSheet**、そのことができます。

    -   いずれかを使用して、 [CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)、定義済みの標準的なページは、そのプリンターを入力するかを指定するインターフェイスの Dll がプリンターのプロパティ シートを使用できます。
    -   一連のユーザーが変更可能な指定[プロパティ シート オプション](property-sheet-options.md)ページに表示されます。
    -   指定、[ページ イベント コールバック](page-event-callbacks.md)関数 CPSUI を呼び出すときに、ユーザーを表示またはページのオプションを変更します。
-   PROPSHEETPAGE 構造体を指定します。

    COMPROPSHEETUI 構造体を使用する場合に使用できる一般的な (標準) ダイアログ ボックスを使用して、ページを構築できない場合、プロパティ シート ページを記述する (Microsoft Windows SDK のドキュメントで説明) PROPSHEETPAGE 構造体を使用できます。 プリンターのインターフェイスの Dll は、通常、このメソッドを使用するは必要ありません。

-   コールバック関数を指定します。

    アプリケーションに渡すことができます[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)のアドレスを[ **PFNPROPSHEETUI**](https://msdn.microsoft.com/library/windows/hardware/ff559812)-コールバック関数では、どの CPSUI をすぐに型指定されました。呼び出されます。 コールバック関数が呼び出し元の責任**ComPropSheet**自体と、プロパティ シートのページを作成します。

    印刷スプーラをプリンター インターフェイス DLL の CPSUI の存在を通知するためにこのメソッドを使用して**DrvDocumentPropertySheets**と*Pscript*ドライバー CPSUIの存在を通知するために、この手法を使用して[**IPrintOemUI::DocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554173)と[ **IPrintOemUI::DevicePropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554165)内の COM メソッド[ユーザープラグインのインターフェイス](user-interface-plug-ins.md)します。

新しいページを指定する方法のいずれかを使用すると、ページ割り当てる必要があります、[グループの親](group-parent.md)へのハンドルの親グループに渡すことによって、 **ComPropSheet**関数。

 

 




