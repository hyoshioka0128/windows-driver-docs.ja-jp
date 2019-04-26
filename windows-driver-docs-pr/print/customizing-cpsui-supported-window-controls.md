---
title: CPSUI 指定のウィンドウ コントロールをカスタマイズする
description: CPSUI 指定のウィンドウ コントロールをカスタマイズする
ms.assetid: b9ced902-6368-4b3b-a974-81e7d38c0ced
keywords:
- 共通のプロパティ シートのユーザー インターフェイスを WDK の印刷、ウィンドウ コントロール
- ウィンドウ コントロールの印刷、CPSUI WDK
- WDK プロパティ シートのページを印刷するウィンドウのコントロール
- WDK CPSUI を制御するウィンドウ
- カスタマイズ ウィンドウの CPSUI でサポートされているコントロール WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c21e159da744343971dec67a4d3fcc104bd50c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355680"
---
# <a name="customizing-cpsui-supported-window-controls"></a>CPSUI 指定のウィンドウ コントロールをカスタマイズする





使用する場合[CPSUI でサポートされているウィンドウ コントロール](cpsui-supported-window-controls.md)と共に[CPSUI が指定したページやテンプレート](cpsui-supplied-pages-and-templates.md)、CPSUI できる方法でコントロールを説明するウィンドウ コントロールのリソースを提供します。連携すること。 そのため、リソース コントロールを提供する必要はありません。

その一方で、CPSUI が指定したページまたはテンプレートを使用しないプロパティ シート ページを作成する場合は、CPSUI でサポートされているウィンドウのコントロールを使用をカスタマイズする必要があります。 これを行うには、ウィンドウ コントロールのリソースを提供する必要があります、 [CPSUI オプションの種類](https://msdn.microsoft.com/library/windows/hardware/ff547142)します。 使用してこれらのリソースの識別子を指定する必要があります、 **BegCtrlID**の各オプションのメンバー [ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体。

ウィンドウの CPSUI でサポートされているコントロールをカスタマイズする場合は、エントリの場合、CPSUI はオプションが表示されませんを注意してください、OPTIF\_で非表示にするフラグを設定、 [ **OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)構造体。 CPSUI では、非表示のオプションが通常占有する領域を埋める、残りのコントロールを移動します。 そのため、同時に表示されているいくつかのオプションを含むページを作成する場合、次の規則は obeyed する必要があります。

-   各オプションは、プロパティ シートのページの全体の水平方向の領域を占有する必要があります。

-   オプションのダイアログ ボックスでは、他のオーバーレイする必要がありますいないします。

-   オプションは、左から右に配置するラジオ ボタンで表される、ボタンとアイコンを x 軸にアラインする必要があります。 場合は、ボタンは、上から下に配置は、ボタンとアイコンは、y 軸の配置する必要があります。

-   グループ ボックスが属する必要がありますをいくつかの項目が 1 つのグループ ボックスを共有する場合、最初に[ **OPTITEM**](https://msdn.microsoft.com/library/windows/hardware/ff559656)、グループ ボックスの最上位の項目であります。 グループ ボックスは、関連付けられているすべての項目を格納するのに十分な大きさである必要があります。

また、オプション ボタンとアイコンは、上から下へとこれらのコントロールの一部が非表示に配置されているが場合、CPSUI は y 方向の結果として得られる空白をしないに削除するは注意してください。

 

 




