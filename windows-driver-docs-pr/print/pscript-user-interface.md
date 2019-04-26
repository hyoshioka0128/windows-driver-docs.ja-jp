---
title: Pscript ユーザー インターフェイス
description: Pscript ユーザー インターフェイス
ms.assetid: 88c1bb99-bc05-454f-ae36-722e9aa246c6
keywords:
- PostScript プリンター ドライバー WDK の印刷、ユーザー インターフェイス
- Pscript WDK 印刷、ユーザー インターフェイス
- WDK Pscript のユーザー インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c9a2026fcaae51e246fbe08d6a55538b45e280
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359017"
---
# <a name="pscript-user-interface"></a>Pscript ユーザー インターフェイス





Pscript ユーザー インターフェイスを採用しています[CPSUI](common-property-sheet-user-interface.md)次のプロパティ シートのページを作成します。

-   **デバイス設定**、ユーザーが選択したときに表示されるプリンターのプロパティ シートのページ、**プロパティ**プリンター フォルダーまたはプリンターのウィンドウからメニュー項目。 ページには、プリンターに固有の構成設定が一覧表示します。

-   **レイアウト**、**用紙/品質**、および**詳細**ユーザーを選択したときに表示されるページ、ドキュメントのプロパティ シートの**印刷設定**プリンター フォルダーまたはプリンターのウィンドウから、またはアプリケーションを呼び出すときにメニュー項目、 **PrinterProperties**または**DocumentProperties**関数 (で説明されている、Microsoft Windows SDK のドキュメント)。 ページは、ドキュメントに固有の構成設定を一覧表示します。

これらのプロパティ シート ページには、プリンターの機能とプリンターの Pscript ミニドライバーで指定されたプリンターのオプションが含まれます。 ユーザー オプション値を変更することもできます。

ユーザー モードとして Pscript ユーザー インターフェイスが実装される[プリンター インターフェイス DLL](printer-interface-dll.md)します。 CPSUI、と共に、この DLL 内のコードでは、プロパティ シートのページの内容を指定します。 DLL は、どのプリンターでオプションを組み合わせて、ミニドライバーの情報に基づいて制約を適用します。 また、ユーザーがプリンターにインストールされていないオプションを選択しないでください。

Pscript が提供するプロパティ シートのページを変更するには、提供する、[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)、というタイトルのセクションに記載されている[をカスタマイズする Microsoft のプリンター ドライバー](customizing-microsoft-s-printer-drivers.md)します。

 

 




