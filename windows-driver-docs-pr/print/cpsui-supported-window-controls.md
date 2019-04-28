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
ms.openlocfilehash: 701bc284d746eaf7e81991bbf94ed4dbade64622
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365579"
---
# <a name="cpsui-supported-window-controls"></a>CPSUI 指定のウィンドウ コントロール





CPSUI には、ユーザーに一貫性のあるインターフェイスを提供するウィンドウ コントロールがサポートされています。 これらのウィンドウ コントロールの使用が特に重要ですプリンター デバイスと、ドキュメントのプロパティ シート ページを作成するときにユーザーが一貫性のあるインターフェイスのすべてのプリンターを期待します。

ウィンドウの CPSUI でサポートされているコントロールは次のとおりです。

-   2 つまたは 3 つのラジオ ボタンを含むボックス

-   スクロールやトラック バー

-   編集、リスト、およびコンボ ボックス

-   上/下の矢印ボックス

-   チェック ボックス

このウィンドウのコントロールのセットは、指定するときに常に使用する必要があります[プロパティ シート オプション](property-sheet-options.md)します。 ウィンドウ コントロールを使用して指定[CPSUI オプションの種類](https://msdn.microsoft.com/library/windows/hardware/ff547142)します。 通常は必要なときに、これらのコントロールの外観をカスタマイズできます。 詳細については、次を参照してください。 [Customizing CPSUI-Supported ウィンドウ コントロール](customizing-cpsui-supported-window-controls.md)します。

CPSUI には、拡張のチェック ボックスと拡張のプッシュ ボタンと呼ばれる、2 つの特殊なコントロールも定義します。 使用して、これらのコントロールでは、標準のチェック ボックスとプッシュ ボタンのもの以外の機能を提供するを指定することができます、 [ **EXTCHKBOX** ](https://msdn.microsoft.com/library/windows/hardware/ff548781)と[ **EXTPUSH**](https://msdn.microsoft.com/library/windows/hardware/ff548795)構造体に、それぞれします。

 

 




