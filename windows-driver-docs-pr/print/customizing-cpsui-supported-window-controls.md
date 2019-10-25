---
title: CPSUI 指定のウィンドウ コントロールをカスタマイズする
description: CPSUI 指定のウィンドウ コントロールをカスタマイズする
ms.assetid: b9ced902-6368-4b3b-a974-81e7d38c0ced
keywords:
- 共通プロパティシートのユーザーインターフェイス WDK 印刷、ウィンドウコントロール
- CPSUI WDK 印刷、ウィンドウコントロール
- プロパティシートページ WDK 印刷、ウィンドウコントロール
- ウィンドウコントロールの WDK CPSUI
- CPSUI でサポートされているウィンドウコントロールのカスタマイズの WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bd0882cb9238b664f30cca1b457c6ac2d16e0b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843377"
---
# <a name="customizing-cpsui-supported-window-controls"></a>CPSUI 指定のウィンドウ コントロールをカスタマイズする





CPSUI でサポートさ[れているウィンドウコントロール](cpsui-supported-window-controls.md)を CPSUI が[提供するページとテンプレート](cpsui-supplied-pages-and-templates.md)と組み合わせて使用している場合、CPSUI には、コントロールをまとめて表示するための方法を説明するウィンドウコントロールリソースが用意されています。 そのため、コントロールにリソースを提供する必要はありません。

一方、CPSUI が提供するページやテンプレートを使用しないプロパティシートページを作成する場合は、使用する CPSUI でサポートされているウィンドウコントロールをカスタマイズする必要があります。 これを行うには、 [CPSUI オプションの種類](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-option-types)のウィンドウコントロールリソースを用意する必要があります。 各オプションの[**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)構造体の**begctrlid**メンバーを使用して、これらのリソースの識別子を指定する必要があります。

CPSUI でサポートされているウィンドウコントロールをカスタマイズしている場合は、OPTIF\_[**Optif**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)構造体で設定されているフラグが非表示になっている場合、CPSUI にはオプションが表示されないことに注意してください。 CPSUI は、残りのコントロールを、hidden オプションによって通常使用される領域を埋めるように移動します。 このため、複数の同時に表示されるオプションを含むページを作成する場合は、次のルールを cache-control する必要があります。

-   各オプションは、プロパティシートページの水平方向の領域全体を占めている必要があります。

-   オプションダイアログは、互いにオーバーレイしてはなりません。

-   左から右に配置されているラジオボタンによって表されるオプションについては、ボタンとアイコンが x 軸に配置されている必要があります。 ボタンが上から下に配置されている場合は、ボタンとアイコンが y 軸に配置されます。

-   複数の項目が1つのグループボックスを共有している場合、グループボックスは、グループボックス内の最上位の項目である最初の[**Optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)に属している必要があります。 グループボックスは、関連付けられているすべての項目を格納するのに十分な大きさである必要があります。

また、オプションボタンとアイコンが上下に並べて表示されていて、これらのコントロールの一部が非表示になっている場合、CPSUI では、y 方向に結果の空白が削除されないことに注意してください。

 

 




