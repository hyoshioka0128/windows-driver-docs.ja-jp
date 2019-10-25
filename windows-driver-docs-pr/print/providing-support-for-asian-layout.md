---
title: アジアのレイアウトのサポートを提供する
description: アジアのレイアウトのサポートを提供する
ms.assetid: 38c7dfca-ce30-4967-84a4-e2f40bba8c57
keywords:
- プリントプロセッサ WDK、アジア言語
- アジア言語の WDK 印刷
- 小冊子 WDK 印刷
- N-up 印刷 WDK
- 逆方向の WDK 印刷
- アラビア語の印刷サポート WDK
- 日本の印刷サポート WDK
- ウルドゥ語印刷サポート WDK
- 国際化に関する考慮事項 WDK
- アジア言語の印刷 (WDK)
- 言語 WDK 印刷
- 右から左への読み取り言語の WDk 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50cb696a1b75f781835f95419b9e7d34374e7819
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840419"
---
# <a name="providing-support-for-asian-layout"></a>アジアのレイアウトのサポートを提供する


Microsoft Windows プリントプロセッサでは、アラビア語、日本語、ウルドゥ語など、右から左に読むアジア言語がサポートされています。次の機能があります。

-   **N アップ方向**: 1 枚のシートに複数のページを印刷する場合、ユーザーはシート上で右から左への順序でページを印刷できます。

-   **小冊子のエッジ**: 小冊子を印刷するときに、シートが折りたたまれ、ページが横に並べて配置されている場合、ユーザーは小冊子ページを右から左に並べて配置できます。 次の図は、小冊子の\_エッジ\_右フラグを使用した、小冊子のページレイアウトを示しています。ブックレット\-edge\-右の](images/asian-booklet.png) フラグを使用して、小冊子のページレイアウトを示す![図

Windows Vista では、アジアのレイアウトをサポートするために、ドライバーの N アップ方向と小冊子端を変更できるフラグが用意されています。 これらの値を設定する方法の詳細については、「 [**DrvQueryJobAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes) and [**ATTRIBUTE\_INFO\_4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/ns-winddiui-_attribute_info_4)」を参照してください。

 

 




