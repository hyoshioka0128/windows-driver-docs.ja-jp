---
title: プロパティシートのオプション
description: プロパティシートのオプション
ms.assetid: 572330d6-1a1b-46fd-bfb4-be2b0990bca4
keywords:
- 共通プロパティシートのユーザーインターフェイス WDK print、プロパティシートオプション
- CPSUI WDK print、プロパティシートオプション
- プロパティシートページの WDK 印刷、プロパティシートのオプション
- プロパティシートの WDK 印刷
- 選択可能なプロパティシートページ項目の WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d897f746ce3950d0d506e1cf7e013f79e227b09
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840423"
---
# <a name="property-sheet-options"></a>プロパティシートのオプション





プロパティシートオプションは、プロパティシートページ上にある、オプションの選択可能な項目です。 通常、ユーザーはオプションの値を変更できます。 CPSUI は、 [CPSUI がサポート](cpsui-supported-window-controls.md)する一連のウィンドウコントロールを使用して、アプリケーションが標準形式でオプションを作成するのに役立ちます。 アプリケーションでは、これらのコントロールにリソースを提供する必要はありません。

各プロパティシートページには、通常、いくつかのオプションが含まれています。 各プロパティシートオプションでは、CPSUI アプリケーションで次の CPSUI 構造体を使用する必要があります。

-   1つの[**Optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)構造体。オプションの表示名とその他の特性を識別します。

-   オプションの display dialog type ([CPSUI option type](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-option-types)) を識別する1つの[**opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)構造体。

-   オプションのユーザーが選択できるパラメーター値を識別する1つ以上の[**Optparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)構造体。

これらの CPSUI 構造体を使用してプロパティシートオプションを記述するには、オプションを含むページを[**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)構造体を使用して定義する必要があります。

 

 




