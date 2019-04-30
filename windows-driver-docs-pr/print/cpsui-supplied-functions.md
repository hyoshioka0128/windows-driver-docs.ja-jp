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
ms.openlocfilehash: d2c04ca8d5507c061effca550a582bbf909a14d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365574"
---
# <a name="cpsui-supplied-functions"></a>CPSUI 指定の関数





CPSUI は、アプリケーションの次の 2 つの重要な機能を提供します。

-   [**CommonPropertySheetUI**](https://msdn.microsoft.com/library/windows/hardware/ff546148)

    [ **CommonPropertySheetUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546148)関数は CPSUI のエントリ ポイント。 関数は、プロパティ シートのページを作成し、表示するには、原因をし、表示し、ユーザーによって変更することができます。

    アプリケーションを呼び出すと[ **CommonPropertySheetUI**](https://msdn.microsoft.com/library/windows/hardware/ff546148)のアドレスを提供、[作成コールバックによってページ](page-creation-callbacks.md)説明ページを作成できます。 CPSUI では、ページの説明を取得するには、このコールバックを呼び出します。 アプリケーションをユーザーに ページに含まれる値の変更を許可し、ページが表示されますおよび配信を使用して、アプリケーションに値を変更する[イベントのコールバックをページ](page-event-callbacks.md)します。 **CommonPropertySheetUI**関数は、ユーザーがクリックして、プロパティ シートを閉じられるまでに返さない**OK**または**キャンセル**します。

    そのプリンターに注意してくださいこの関数を呼び出さない Dll インターフェイス。印刷スプーラーによって呼び出されます。

-   [**ComPropSheet**](https://msdn.microsoft.com/library/windows/hardware/ff546207)

    [ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)関数は、アプリケーションが CPSUI が作成してそれらを表示できるようにする CPSUI、プロパティ シートのページを記述することを意味します。 CPSUI アプリケーション内からこの関数を呼び出す[ページ作成コールバック](page-creation-callbacks.md)します。 通常、ページの説明へのポインターが含まれます。、[ページ イベント コールバック](page-event-callbacks.md)、CPSUI がアプリケーションのユーザーがページの値を変更するときに呼び出されます。

これらの関数が呼び出されるタイミングの詳細については、次を参照してください。[プリンター ドライバーを使用して CPSUI](using-cpsui-with-printer-drivers.md)します。

2 つ追加 CPSUI が提供する機能[ **SetCPSUIUserData** ](https://msdn.microsoft.com/library/windows/hardware/ff562624)と[ **GetCPSUIUserData**](https://msdn.microsoft.com/library/windows/hardware/ff549922)、によって、アプリケーションによって提供されることができます格納し、アプリケーションによって提供される値を取得] ダイアログ ボックス プロシージャ。

 

 




