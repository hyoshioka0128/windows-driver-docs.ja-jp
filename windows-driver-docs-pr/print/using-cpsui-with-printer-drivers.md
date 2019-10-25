---
title: プリンター ドライバーで CPSUI を使用する
description: プリンター ドライバーで CPSUI を使用する
ms.assetid: 898a855d-6a9a-4f98-9ee4-bad439427326
keywords:
- 共通プロパティシートのユーザーインターフェイス WDK 印刷、プロパティシートページの表示
- CPSUI WDK print、プロパティシートページの表示
- プロパティシートページの WDK 印刷、表示
- プロパティシートのページの表示
- 一般的なプロパティシートのユーザーインターフェイス WDK print、CPSUI について
- CPSUI WDK print、CPSUI について
- プロパティシートページ WDK 印刷、CPSUI とプリンタードライバーの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0b454eb7513502f5ba7b6a9efdf6f715d5cf939
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844201"
---
# <a name="using-cpsui-with-printer-drivers"></a>プリンター ドライバーで CPSUI を使用する





印刷スプーラは、[プリンターインターフェイス dll](printer-interface-dll.md)と組み合わせて CPSUI を使用して、印刷ドキュメントとプリンターデバイスのプロパティシートページを作成します。 次の手順は、アプリケーション (Microsoft Word など) によって印刷ドキュメントのプロパティシートが表示される場合に関係します。

1.  アプリケーションは、印刷スプーラの**DocumentProperties**関数 (Microsoft Windows SDK のドキュメントで説明されています) を呼び出して、ドキュメントを印刷するプリンターを指定します。

2.  印刷スプーラは、内部的な[**PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)型のコールバック関数を指定して、CPSUI のエントリポイント関数[**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)を呼び出します。

3.  CPSUI は、スプーラの PFNPROPSHEETUI によって型指定されたコールバック関数を呼び出します。

4.  スプーラの PFNPROPSHEETUI で型指定されたコールバック関数は、CPSUI の[**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)関数 ( [**cpsfunc\_ADD\_PFNPROPSHEETUI**](https://docs.microsoft.com/previous-versions/ff546391(v=vs.85))関数コード) を呼び出して、適切なプリンターインターフェイス DLL[**のアドレスを CPSUI に通知します。DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)関数。

5.  CPSUI は、プリンターインターフェイス DLL の**DrvDocumentPropertySheets**関数を呼び出します。

6.  Printer interface DLL の**DrvDocumentPropertySheets**関数は、CPSUI の**ComPropSheet**関数 (通常は[**cpsfunc\_ADD\_PCOMPROPSHEETUI**](https://docs.microsoft.com/previous-versions/ff546388(v=vs.85))関数コード) を呼び出して、CPSUI をプロパティシートページに提供します。説明と[ページイベントのコールバック](page-event-callbacks.md)。

7.  CPSUI の**ComPropSheet**関数は、 **createpropertysheet ページ**(Windows SDK ドキュメントで説明されています) を呼び出して、プリンターインターフェイス DLL によって指定されたプロパティシートページを作成します。 次に、CPSUI は、プロパティシートのページを表示するために、(Windows SDK のドキュメントで説明されている **) プロパティシートを呼び出します**。

次の図は、これらの手順を示しています。

![プロパティシートの表示に関連するモジュールを示す図](images/usecpsui.png)

アプリケーションユーザーがプロパティシートのページを走査し、オプションの値を変更すると、オペレーティングシステムによって CPSUI のページイベントと CPSUI が通知され、プリンターインターフェイス DLL によって提供されるページイベントコールバックが呼び出されます。 ページイベントコールバックは、ページイベントを処理し、必要に応じて、新しく選択されたオプション値を内部に格納します。

ユーザーが **[Ok]** または **[キャンセル**] ボタンをクリックしてプロパティシートを閉じると、CPSUI によってページが破棄され、 **CommonPropertySheetUI**関数は印刷スプーラに戻り、その後、アプリケーションにコントロールが返されます。

アプリケーションで印刷ドキュメントではなく、プリンターデバイスのプロパティシートが表示される場合も、同じ手順が実行されます。ただし、アプリケーションがスプーラの**Print properties**関数を呼び出し、スプーラーによってプリンターのアドレスが渡される点が異なります。インターフェイス DLL の[**DrvDevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)関数を CPSUI にします。

 

 




