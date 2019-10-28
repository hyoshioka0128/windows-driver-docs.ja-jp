---
title: CPSUI 指定の関数
description: CPSUI 指定の関数
ms.assetid: 49da252a-fb51-43f3-b2e8-27253470b4b5
keywords:
- 一般的なプロパティシートのユーザーインターフェイス WDK print、functions
- CPSUI WDK print、functions
- プロパティシートページ WDK 印刷、関数
- functions WDK CPSUI
- CommonPropertySheetUI
- ComPropSheet
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 524c9497b878ae480ecf96f6651a028cb2dd8d55
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843062"
---
# <a name="cpsui-supplied-functions"></a>CPSUI 指定の関数





CPSUI は、次の2つの重要な機能をアプリケーションに提供します。

-   [**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)

    [**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)関数は CPSUI のエントリポイントです。 関数を使用すると、プロパティシートのページが作成されて表示され、ユーザーが表示および変更できるようになります。

    アプリケーションが[**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)を呼び出すと、作成されるページを説明する[ページ作成コールバック](page-creation-callbacks.md)のアドレスが提供されます。 CPSUI は、このコールバックを呼び出してページの説明を取得します。 次に、ページを表示し、アプリケーションユーザーがページに含まれる値を変更し、[ページイベントコールバック](page-event-callbacks.md)を使用して変更された値をアプリケーションに配信できるようにします。 **CommonPropertySheetUI**関数は、ユーザーが [ **OK]** または **[キャンセル**] をクリックしてプロパティシートを閉じない限り、を返しません。

    プリンターインターフェイス Dll はこの関数を呼び出しません。これは、印刷スプーラによって呼び出されます。

-   [**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)

    [**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)関数は、アプリケーションが CPSUI にプロパティシートページを記述し、CPSUI がそれらを作成して表示できるようにするための手段です。 CPSUI アプリケーションは、[ページ作成コールバック](page-creation-callbacks.md)内からこの関数を呼び出します。 通常、ページの説明には、ページ[イベントコールバック](page-event-callbacks.md)へのポインターが含まれます。これは、アプリケーションユーザーがページ値を変更したときに CPSUI によって呼び出されます。

これらの関数が呼び出されるタイミングの詳細については、「 [CPSUI とプリンタードライバーの使用](using-cpsui-with-printer-drivers.md)」を参照してください。

CPSUI に用意されている2つの関数[**setcpsuiuserdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-setcpsuiuserdata)と[**Getcpsuiuserdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nf-compstui-getcpsuiuserdata)は、アプリケーションによって提供される値を格納および取得するために、アプリケーションによって提供されるダイアログボックスプロシージャで使用できます。

 

 




