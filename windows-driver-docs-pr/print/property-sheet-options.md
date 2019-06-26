---
title: プロパティ シート オプション
description: プロパティ シート オプション
ms.assetid: 572330d6-1a1b-46fd-bfb4-be2b0990bca4
keywords:
- 共通のプロパティ シートのユーザー インターフェイスを WDK の印刷、プロパティ シートのオプション
- CPSUI WDK 印刷、プロパティ シートのオプション
- WDK プロパティ シートのページの印刷、プロパティ シートのオプション
- WDK のプロパティ シートを印刷します。
- 選択可能なプロパティ シート ページ項目 WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c3daf9f4a1554970fcaa231028ebdd9f6a06af9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356021"
---
# <a name="property-sheet-options"></a>プロパティ シート オプション





プロパティ シートのオプションは、プロパティ シートのページで選択可能な表示可能な項目です。 通常、ユーザーは、オプションの値を変更できます。 CPSUI により、標準の形式での作成オプションのアプリケーションの定義済みセットを使用して[CPSUI でサポートされているウィンドウ コントロール](cpsui-supported-window-controls.md)します。 アプリケーションをこれらのコントロールのリソースを提供する必要はありません。

通常、各プロパティ ページには、いくつかのオプションが含まれています。 プロパティ シートのオプションごとに CPSUI アプリケーションは、次の CPSUI 構造を使用する必要があります。

-   1 つ[ **OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)構造体は、オプションの表示名とその他の特性を識別します。

-   1 つ[ **OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)オプションの表示 ダイアログの種類を識別する構造体 ([CPSUI オプションの種類](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-option-types))。

-   1 つまたは複数[ **OPTPARAM$** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optparam)構造体は、オプションのユーザーが選択可能なパラメーターの値を識別します。

これらの CPSUI 構造体を使用して、プロパティ シートのオプションについて説明する、オプションが含まれるページを使用して、 [ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)構造体。

 

 




