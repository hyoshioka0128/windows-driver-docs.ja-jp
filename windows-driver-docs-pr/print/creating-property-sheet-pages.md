---
title: プロパティ シート ページを作成する
description: プロパティ シート ページを作成する
ms.assetid: 90b1743c-b530-408a-aa30-9ab774166306
keywords:
- 共通のプロパティ シートのユーザー インターフェイスを WDK の印刷、プロパティ シートのページを作成します。
- CPSUI WDK の印刷、プロパティ シートのページを作成します。
- WDK のプロパティ シート ページが印刷を作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba1a9bd3f897bcb8910653c109bfbe1a0ae512b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372432"
---
# <a name="creating-property-sheet-pages"></a>プロパティ シート ページを作成する





CPSUI を使用して作成されたプロパティ シートのページが作られる[プロパティ シート オプション](property-sheet-options.md)、各オプションがユーザーが変更可能な値を表します。 ダイアログ ボックスのセットを使用してプロパティ シートのオプションが作成されたの[CPSUI でサポートされているウィンドウ コントロール](cpsui-supported-window-controls.md)オプションの値を変更することができます。

内で CPSUI が指定したウィンドウのコントロールを表示できる[CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)、カスタマイズされたページを使用することができます。 いくつか[ページを指定するためのメソッド](methods-for-specifying-pages.md)、CPSUI の呼び出しが含まれるすべての[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)関数。

プリンターおよび印刷するドキュメントのプロパティ シートのページを作成するには[CPSUI を使用してプリンター ドライバーで](using-cpsui-with-printer-drivers.md)アプリケーション、印刷スプーラー、プリンター インターフェイス DLL、および CPSUI 間の相互作用する必要があります。

 

 




