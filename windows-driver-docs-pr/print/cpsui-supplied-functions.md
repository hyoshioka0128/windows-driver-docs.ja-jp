---
title: CPSUI 指定の関数
description: CPSUI 指定の関数
ms.assetid: 49da252a-fb51-43f3-b2e8-27253470b4b5
keywords:
- 共通のプロパティ シートのユーザー インターフェイスの WDK 印刷、関数
- CPSUI WDK の印刷、関数
- WDK プロパティ シートのページを印刷する関数
- WDK CPSUI 関数
- CommonPropertySheetUI
- ComPropSheet
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a322d252fd40d8b85afff9c9f644355fbc2f6b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372444"
---
# <a name="cpsui-supplied-functions"></a>CPSUI 指定の関数





CPSUI は、アプリケーションの次の 2 つの重要な機能を提供します。

-   [**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)

    [ **CommonPropertySheetUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)関数は CPSUI のエントリ ポイント。 関数は、プロパティ シートのページを作成し、表示するには、原因をし、表示し、ユーザーによって変更することができます。

    アプリケーションを呼び出すと[ **CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia)のアドレスを提供、[作成コールバックによってページ](page-creation-callbacks.md)説明ページを作成できます。 CPSUI では、ページの説明を取得するには、このコールバックを呼び出します。 アプリケーションをユーザーに ページに含まれる値の変更を許可し、ページが表示されますおよび配信を使用して、アプリケーションに値を変更する[イベントのコールバックをページ](page-event-callbacks.md)します。 **CommonPropertySheetUI**関数は、ユーザーがクリックして、プロパティ シートを閉じられるまでに返さない**OK**または**キャンセル**します。

    そのプリンターに注意してくださいこの関数を呼び出さない Dll インターフェイス。印刷スプーラーによって呼び出されます。

-   [**ComPropSheet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)

    [ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)関数は、アプリケーションが CPSUI が作成してそれらを表示できるようにする CPSUI、プロパティ シートのページを記述することを意味します。 CPSUI アプリケーション内からこの関数を呼び出す[ページ作成コールバック](page-creation-callbacks.md)します。 通常、ページの説明へのポインターが含まれます。、[ページ イベント コールバック](page-event-callbacks.md)、CPSUI がアプリケーションのユーザーがページの値を変更するときに呼び出されます。

これらの関数が呼び出されるタイミングの詳細については、次を参照してください。[プリンター ドライバーを使用して CPSUI](using-cpsui-with-printer-drivers.md)します。

2 つ追加 CPSUI が提供する機能[ **SetCPSUIUserData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-setcpsuiuserdata)と[ **GetCPSUIUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-getcpsuiuserdata)、によって、アプリケーションによって提供されることができます格納し、アプリケーションによって提供される値を取得] ダイアログ ボックス プロシージャ。

 

 




