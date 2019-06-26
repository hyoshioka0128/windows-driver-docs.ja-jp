---
title: プリンター ドライバーで CPSUI を使用する
description: プリンター ドライバーで CPSUI を使用する
ms.assetid: 898a855d-6a9a-4f98-9ee4-bad439427326
keywords:
- 共通のプロパティ シートのユーザー インターフェイスを WDK の印刷、プロパティ シートのページを表示します。
- CPSUI WDK の印刷、プロパティ シートのページを表示します。
- WDK プロパティ シートのページの印刷、表示します。
- プロパティ シートのページを表示します。
- 一般的なプロパティ シートのユーザー インターフェイス WDK CPSUI についての印刷
- CPSUI WDK CPSUI についての印刷
- WDK プロパティ シートのページを印刷するプリンター ドライバーで CPSUI について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf4ae849bf9db95797a2bc59d8f051c6a4f28a5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384171"
---
# <a name="using-cpsui-with-printer-drivers"></a>プリンター ドライバーで CPSUI を使用する





組み合わせて、印刷スプーラー[プリンター インターフェイス Dll](printer-interface-dll.md)CPSUI を使用して印刷するドキュメントとプリンター デバイスのプロパティ シート ページを作成します。 (Microsoft Word の場合) などのアプリケーションは、印刷ドキュメントのプロパティ シートを表示するとき、次の手順が含まれます。

1.  アプリケーションは、印刷スプーラーを呼び出して**DocumentProperties**関数 (Microsoft Windows SDK のドキュメントで説明)、ドキュメントを印刷するプリンターを指定します。

2.  印刷スプーラが CPSUI のエントリ ポイント関数を呼び出す[ **CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)、内部を指定する[ **PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfnpropsheetui)-型指定されたコールバック関数。

3.  CPSUI では、スプーラーの PFNPROPSHEETUI に型指定されたコールバック関数を呼び出します。

4.  スプーラの PFNPROPSHEETUI に型指定されたコールバック関数によって CPSUI の[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)関数 (で、 [ **CPSFUNC\_追加\_PFNPROPSHEETUI** ](https://docs.microsoft.com/previous-versions/ff546391(v=vs.85))機能コード) に、適切なプリンター インターフェイスの DLL のアドレスの CPSUI を通知する[ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)関数。

5.  CPSUI インターフェイスを呼び出し、プリンター DLL の**DrvDocumentPropertySheets**関数。

6.  プリンター インターフェイス DLL の**DrvDocumentPropertySheets**関数 CPSUI の**ComPropSheet**関数 (通常、 [ **CPSFUNC\_の追加\_PCOMPROPSHEETUI** ](https://docs.microsoft.com/previous-versions/ff546388(v=vs.85))機能コード) プロパティ シート ページの説明に CPSUI を提供して[イベントのコールバックをページ](page-event-callbacks.md)します。

7.  CPSUI の**ComPropSheet**関数呼び出し**CreatePropertySheetPage** (Windows SDK のドキュメントで説明)、プリンター インターフェイス DLL で指定されたプロパティ シートのページを作成します。 CPSUI を呼び出して**プロパティ シート**(Windows SDK のドキュメントで説明) プロパティ シートのページを表示します。

次の図は、次の手順を示します。

![プロパティ シートの表示に必要なモジュールを示す図](images/usecpsui.png)

アプリケーションのユーザーは、プロパティ シートのページを通過し、オプションの値を変更、オペレーティング システムに通知のページ イベント CPSUI と CPSUI、さらに、プリンター インターフェイス DLL によって指定されたページ イベント コールバックを呼び出します。 ページのイベントのコールバックは、ページ イベントを処理し、ストア新しく選択したオプション値を内部的には、必要に応じて。

クリックして、ユーザーがプロパティ シートを閉じるときに、 **Ok**または**キャンセル**CPSUI ボタンがページを破棄し、原因、 **CommonPropertySheetUI**を返す関数印刷スプーラーをし、アプリケーションにコントロールを返します。

アプリケーションでは、印刷ドキュメントではなくプリンター デバイスのプロパティ シートを表示するとき、同じ手順が、アプリケーションが呼び出す、スプーラーのことを除いて**PrinterProperties**関数とスプーラー パス、プリンターのインターフェイスのアドレス DLL の[ **DrvDevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets) CPSUI する関数。

 

 




