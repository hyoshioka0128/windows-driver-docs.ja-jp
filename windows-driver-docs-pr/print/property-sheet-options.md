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
ms.openlocfilehash: 9300f4410fe2e00dea4e7805d3cf8db7b815efd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578448"
---
# <a name="property-sheet-options"></a>プロパティ シート オプション





プロパティ シートのオプションは、プロパティ シートのページで選択可能な表示可能な項目です。 通常、ユーザーは、オプションの値を変更できます。 CPSUI により、標準の形式での作成オプションのアプリケーションの定義済みセットを使用して[CPSUI でサポートされているウィンドウ コントロール](cpsui-supported-window-controls.md)します。 アプリケーションをこれらのコントロールのリソースを提供する必要はありません。

通常、各プロパティ ページには、いくつかのオプションが含まれています。 プロパティ シートのオプションごとに CPSUI アプリケーションは、次の CPSUI 構造を使用する必要があります。

-   1 つ[ **OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)構造体は、オプションの表示名とその他の特性を識別します。

-   1 つ[ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)オプションの表示 ダイアログの種類を識別する構造体 ([CPSUI オプションの種類](https://msdn.microsoft.com/library/windows/hardware/ff547142))。

-   1 つまたは複数[ **OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)構造体は、オプションのユーザーが選択可能なパラメーターの値を識別します。

これらの CPSUI 構造体を使用して、プロパティ シートのオプションについて説明する、オプションが含まれるページを使用して、 [ **COMPROPSHEETUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546211)構造体。

 

 




