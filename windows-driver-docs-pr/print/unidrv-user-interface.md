---
title: Unidrv ユーザー インターフェイス
description: Unidrv ユーザー インターフェイス
ms.assetid: b1f34ebf-8c8a-4b43-ba48-26bcf6352360
keywords:
- Unidrv、ユーザー インターフェイス
- WDK Unidrv のユーザー インターフェイス
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80eac4b200fe578cd9e4a2a8214fe41096f04719
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346530"
---
# <a name="unidrv-user-interface"></a>Unidrv ユーザー インターフェイス





Unidrv ユーザー インターフェイスを採用しています[CPSUI](common-property-sheet-user-interface.md)次のプロパティ シートのページを作成します。

-   **デバイス設定**、ユーザーが選択したときに表示されるプリンターのプロパティ シートのページ、**プロパティ**プリンター フォルダーまたはプリンターのウィンドウからメニュー項目。 ページには、プリンターに固有の構成設定が一覧表示します。

-   **レイアウト**、**用紙/品質**、および**詳細**ユーザーを選択したときに表示される、ドキュメントのプロパティ シートのページ、**ドキュメントの既定値**プリンター フォルダーまたはプリンターのウィンドウから、またはアプリケーションを呼び出すときにメニュー項目、 **PrinterProperties**または**DocumentProperties**関数 (で説明されている、Microsoft Windows SDK のドキュメント)。 ページは、ドキュメントに固有の構成設定を一覧表示します。

これらのプロパティ シート ページが含まれて、[プリンターの機能](printer-features.md)と[プリンター オプション](printer-options.md)プリンターの Unidrv ミニドライバーで指定します。 ユーザー オプション値を変更することもできます。

ユーザー モードとして Unidrv ユーザー インターフェイスが実装される[プリンター インターフェイス DLL](printer-interface-dll.md)します。 CPSUI、と共に、この DLL 内のコードでは、プロパティ シートのページの内容を指定します。 DLL は、どのプリンターでオプションを組み合わせて、ミニドライバーの情報に基づいて制約を適用します。 また、ユーザーがプリンターにインストールされていないオプションを選択しないでください。

Unidrv が提供するプロパティ シートのページを変更するには、提供する、[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)します。

 

 




