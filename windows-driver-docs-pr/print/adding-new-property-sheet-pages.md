---
title: 新しいプロパティ シートのページを追加する
description: 新しいプロパティ シートのページを追加する
ms.assetid: ec4303e9-889c-41ee-8872-ddefdc906eb2
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、プロパティ シート ページ
- UI プラグインを WDK の印刷、プロパティ シートのページ
- WDK プロパティ シートのページを印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 884ec86b72b32f10aa8d0262614eb09b862523dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354094"
---
# <a name="adding-new-property-sheet-pages"></a>新しいプロパティ シートのページを追加する





新しいページを Unidrv または Pscript5、プラグイン UI プリンター インターフェイスによって提供されるプロパティ シートを追加する場合は、次の IPrintOemUI メソッドを実装する必要があります。

-   [**IPrintOemUI::DevicePropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff554165)

    ユーザーが選択したときに表示されるプリンターのプロパティ シートに追加するために使用、**プロパティ**プリンター フォルダーまたはプリンターのウィンドウから、または、アプリケーションが PrinterProperties 関数を呼び出すときにメニュー項目 (で説明されている、Windows SDK ドキュメント)。

-   [**IPrintOemUI::DocumentPropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff554173)

    ユーザーが選択したときに表示されるドキュメントのプロパティ シートにページを追加するために使用、**プリンターの設定**プリンター フォルダーまたはプリンターのウィンドウから、またはアプリケーションを呼び出すと、DocumentProperties メニュー項目または(Windows SDK のドキュメントで説明した) AdvancedDocumentProperties 関数。

これらのメソッドを実装する場合は通常も指定する、 [  **\_CPSUICALLBACK**](https://msdn.microsoft.com/library/windows/hardware/ff564313)-ユーザーによる変更を処理するコールバック関数を入力します。 このコールバック関数を呼び出す必要があります[ **IPrintOemDriverUI::DrvUpdateUISetting** ](https://msdn.microsoft.com/library/windows/hardware/ff553115)設定の値がある場合、ユーザー インターフェイスの設定に関連付けられた値が変更されたときに、ドライバーに通知するにはドライバーに格納されている[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体またはレジストリのキー。

 

 




