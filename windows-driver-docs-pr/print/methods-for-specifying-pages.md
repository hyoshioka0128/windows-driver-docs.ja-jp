---
title: ページを指定するためのメソッド
description: ページを指定するためのメソッド
ms.assetid: 76006a2b-37b9-4490-913e-dcfc01812d43
keywords:
- 共通プロパティシートのユーザーインターフェイス WDK 印刷、ページの指定
- CPSUI WDK print、ページの指定
- プロパティシートページの WDK 印刷、指定
- COMPROPSHEETUI
- PROPSHEET ページ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be5aabb12302a4ba4006e17ddf77a490a8e99e41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841644"
---
# <a name="methods-for-specifying-pages"></a>ページを指定するためのメソッド





アプリケーションでは、3つの方法のいずれかを使用して、CPSUI するプロパティシートページを指定できます。 次の各メソッドでは、いずれかの[ComPropSheet 関数コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)を指定して、CPSUI の[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)関数を呼び出します。

-   [**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)構造体の提供

    アプリケーションで、COMPROPSHEETUI 構造体を**ComPropSheet**に渡すことによってプロパティシートページを記述する場合、次のことが可能です。

    -   CPSUI に用意されている[ページとテンプレート](cpsui-supplied-pages-and-templates.md)のいずれかを使用して、プリンターインターフェイス dll がプリンタープロパティシートに使用できる定義済みの標準ページの種類を指定します。
    -   ページに表示される、ユーザーが変更可能な[プロパティシートのオプション](property-sheet-options.md)のセットを指定します。
    -   ユーザーがページのオプションを表示または変更したときに CPSUI が呼び出す[ページイベントコールバック](page-event-callbacks.md)関数を指定します。
-   PROPSHEET ページ構造の提供

    COMPROPSHEETUI 構造体を使用しているときに使用できるコモン (標準) ダイアログを使用してページを作成できない場合は、(Microsoft Windows SDK のドキュメントで説明されている) PROPSHEET ページ構造を使用してプロパティシートページを記述できます。 通常、プリンターインターフェイス Dll では、このメソッドを使用する必要はありません。

-   コールバック関数の提供

    アプリケーションは、 [**PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)で指定されたコールバック関数のアドレスを[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)に渡すことができます。この関数は、すぐにを呼び出します。 コールバック関数は、プロパティシートページを作成するために**ComPropSheet**自体を呼び出す役割を担います。

    印刷スプーラでは、このメソッドを使用して CPSUI の存在を通知し:D ます。プリンターインターフェイス DLL の**DrvDocumentPropertySheets**と*pscript*ドライバは、Iprintoemui の存在を CPSUI に通知する技法を使用し[**ます。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)および[**Iprintoemui::D**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets) [ユーザーインターフェイスプラグイン](user-interface-plug-ins.md)で evicepropertysheets COM メソッドを実行します。

新しいページを指定するためにどの方法を使用する場合でも、グループの親ハンドルを**ComPropSheet**関数に渡すことによって、ページを[グループの親](group-parent.md)に割り当てる必要があります。

 

 




