---
title: CPSUI 指定のウィンドウ コントロール
description: CPSUI 指定のウィンドウ コントロール
ms.assetid: 557aa4e6-e48e-44fe-b833-93728426b056
keywords:
- 共通のプロパティ シートのユーザー インターフェイスを WDK の印刷、ウィンドウ コントロール
- ウィンドウ コントロールの印刷、CPSUI WDK
- WDK プロパティ シートのページを印刷するウィンドウのコントロール
- WDK CPSUI を制御するウィンドウ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba50584d1175f17860d5e541d5a890fcc9793c5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372440"
---
# <a name="cpsui-supported-window-controls"></a>CPSUI 指定のウィンドウ コントロール





CPSUI には、ユーザーに一貫性のあるインターフェイスを提供するウィンドウ コントロールがサポートされています。 これらのウィンドウ コントロールの使用が特に重要ですプリンター デバイスと、ドキュメントのプロパティ シート ページを作成するときにユーザーが一貫性のあるインターフェイスのすべてのプリンターを期待します。

ウィンドウの CPSUI でサポートされているコントロールは次のとおりです。

-   2 つまたは 3 つのラジオ ボタンを含むボックス

-   スクロールやトラック バー

-   編集、リスト、およびコンボ ボックス

-   上/下の矢印ボックス

-   チェック ボックス

このウィンドウのコントロールのセットは、指定するときに常に使用する必要があります[プロパティ シート オプション](property-sheet-options.md)します。 ウィンドウ コントロールを使用して指定[CPSUI オプションの種類](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-option-types)します。 通常は必要なときに、これらのコントロールの外観をカスタマイズできます。 詳細については、次を参照してください。 [Customizing CPSUI-Supported ウィンドウ コントロール](customizing-cpsui-supported-window-controls.md)します。

CPSUI には、拡張のチェック ボックスと拡張のプッシュ ボタンと呼ばれる、2 つの特殊なコントロールも定義します。 使用して、これらのコントロールでは、標準のチェック ボックスとプッシュ ボタンのもの以外の機能を提供するを指定することができます、 [ **EXTCHKBOX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_extchkbox)と[ **EXTPUSH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_extpush)構造体に、それぞれします。

 

 




