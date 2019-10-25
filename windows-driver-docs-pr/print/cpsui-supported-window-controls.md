---
title: CPSUI 指定のウィンドウ コントロール
description: CPSUI 指定のウィンドウ コントロール
ms.assetid: 557aa4e6-e48e-44fe-b833-93728426b056
keywords:
- 共通プロパティシートのユーザーインターフェイス WDK 印刷、ウィンドウコントロール
- CPSUI WDK 印刷、ウィンドウコントロール
- プロパティシートページ WDK 印刷、ウィンドウコントロール
- ウィンドウコントロールの WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f64108ddd300d18c667b3b01ba7a2c21c506d63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827457"
---
# <a name="cpsui-supported-window-controls"></a>CPSUI 指定のウィンドウ コントロール





CPSUI は、ユーザーに一貫したインターフェイスを提供する一連のウィンドウコントロールをサポートしています。 これらのウィンドウコントロールの使用は、プリンターデバイスとドキュメントのプロパティシートページを作成するときに特に重要です。ユーザーは、すべてのプリンターに対して一貫したインターフェイスを期待します。

CPSUI でサポートされているウィンドウコントロールは次のとおりです。

-   2つまたは3つのラジオボタンを含むボックス

-   スクロールバーとトラックバー

-   エディットボックス、リスト、コンボボックス

-   上/下矢印ボックス

-   チェックボックス

この一連のウィンドウコントロールは、[プロパティシートオプション](property-sheet-options.md)を指定するときに常に使用する必要があります。 ウィンドウコントロールは、 [CPSUI オプションの種類](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-option-types)を使用して指定します。 通常は必要ありませんが、これらのコントロールの外観はカスタマイズできます。 詳細については、「 [CPSUI でサポートされているウィンドウコントロールのカスタマイズ](customizing-cpsui-supported-window-controls.md)」を参照してください。

CPSUI では、拡張チェックボックスと拡張プッシュボタンと呼ばれる、2つの特殊なコントロールも定義されています。 これらのコントロールは、標準のチェックボックスやプッシュボタン以外の機能を提供します。これらのコントロールは、それぞれ[**EXTCHKBOX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_extchkbox)および[**extpush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_extpush)構造体を使用して指定できます。

 

 




