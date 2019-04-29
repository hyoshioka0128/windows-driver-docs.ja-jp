---
title: デバイスのプロパティ ページのプロバイダーの一般的な要件
description: デバイスのプロパティ ページのプロバイダーの一般的な要件
ms.assetid: 91e93679-8c0c-43e7-a7d9-72bd0a464406
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d1d72eef250a6128c519ec3f4ea893dbe872307
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392509"
---
# <a name="general-requirements-for-device-property-page-providers"></a>デバイスのプロパティ ページのプロバイダーの一般的な要件


デバイスのプロパティ ページを作成するには、プロバイダーは正常に動作するプロパティ ページの順序でこれらの一般的な要件に従う必要があります。

-   プロパティ ページを追加する要求を処理します。

    この要求が行われるプロバイダーのプロパティ ページの拡張 Dll である場合、 **AddPropSheetPageProc**コールバック関数。 詳細については、次を参照してください[デバイス プロパティ ページのプロバイダー (プロパティ ページの拡張 Dll) の特定の要件。](specific-requirements-for-device-property-page-providers--property-pag.md)

-   呼び出して、プロパティ ページを作成、 **CreatePropertySheetPage**関数。 プロバイダーは、この呼び出しで初期化された PROPSHEETPAGE 構造体のアドレスを渡します。

-   指定、 **PropSheetPageProc** PSPCB_CREATE および PSPCB_RELEASE を処理するコールバック関数メッセージの場合、追加のストレージを割り当てられ、プロパティ ページを解放する必要があります。

-   各カスタム プロパティ ページの Windows メッセージを処理する ダイアログ ボックス プロシージャを指定します。
-   Initialize を PROPSHEETPAGE 構造体 (特に) のアドレス、 **PropSheetPageProc**コールバック関数とダイアログ ボックス プロシージャ。

このセクションには、カスタム プロパティ ページについて詳しく説明する次のトピックが含まれています。

[カスタム プロパティ ページを作成します。](creating-custom-property-pages.md)

[プロパティ ページのコールバック関数](property-page-callback-function.md)

[プロパティ ページの Windows メッセージの処理](handling-windows-messages-for-property-pages.md)

[サンプルのカスタム プロパティ ページ](sample-custom-property-page.md)

 

 





