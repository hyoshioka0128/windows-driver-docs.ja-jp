---
title: NDIS ドライバー スタック
description: NDIS ドライバー スタック
ms.assetid: 38302f1e-9b5a-4fc5-8e69-888929e5a892
keywords:
- ドライバー スタックの WDK ネットワー キング、NDIS 基本的な構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 359ad690544d057eebc7874646ca932ca50ed8ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392990"
---
# <a name="ndis-driver-stack"></a>NDIS ドライバー スタック





### <a name="basic-stack-configuration"></a>基本的なスタックの構成

次の図は、NDIS 6.0 のドライバー スタックでの論理要素の基本構成を示します。 フィルター モジュール数が指定されていないドライバー スタックの図に示します。 矢印は、スタックの要素間の情報フローを表します。

![フィルター モジュールでの ndis ドライバー スタックを示す図](images/filterstack.png)

上記の図に示すようミニポート アダプタ上でフィルター モジュールの任意の数をスタックできます。 これらのモジュールには、別のフィルター ドライバーのインスタンスや同じフィルター ドライバーの複数のインスタンスを指定できます。 ミニポート ドライバーでは、ミニポート アダプターが 1 つ以上を管理している場合は、個別のドライバー スタックが各ミニポート アダプタ上で存在できます。

プロトコル ドライバーは、ミニポート アダプターにバインドします。 そのため、ドライバー スタック内の基になるフィルター モジュールは、プロトコル ドライバーに透過的です。 基になるフィルター モジュールに関する情報を取得するには、プロトコルのドライバーがドライバー スタック内のフィルター モジュールを列挙できます。

プロトコルの 1 つ以上のドライバーは、ミニポート アダプターにバインドした場合、フィルター モジュールは両方のプロトコル ドライバーのと同じになります。 NDIS は、バインディングに基づいて、適切なプロトコル ドライバーに要求をルーティングします。

### <a href="" id="ndis-6-0-stack-with-intermediate-driver"></a>NDIS 6.0 の中間のドライバーを使用したスタック

次の図には、中間のドライバーを使用した、NDIS 6.0 のドライバー スタックが表示されます。

![中間のドライバーを使用した、ndis ドライバー スタックを示す図](images/imstack.png)

NDIS 中間ドライバーをドライバー スタックに含める場合は、スタックは基本的に 2 つのスタック。 隣接します。

仮想ミニポートのドライバーの中間は、中間ドライバーのプロトコルのエッジは、下位のスタックのプロトコル バインドを提供します。 一方、上位のスタックのミニポート アダプターを提供します。

仮想ミニポートでは、その他のミニポート アダプターと同じ状態があります。 ミニポート アダプタの状態の詳細については、次を参照してください。[ミニポート ドライバーのアダプター状態](adapter-states-of-a-miniport-driver.md)します。

中間ドライバーのプロトコルの端には、プロトコル ドライバーとして同じバインドの状態を実装する必要があります。 バインドの状態の詳細については、次を参照してください。[プロトコル ドライバーのバインド状態](binding-states-of-a-protocol-driver.md)します。

## <a name="related-topics"></a>関連トピック


[ミニポート ドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[バインディング プロトコル ドライバーの状態](binding-states-of-a-protocol-driver.md)

[ドライバー スタックの管理](driver-stack-management.md)

[NDIS フィルター ドライバー](ndis-filter-drivers.md)

[NDIS 中間ドライバ](ndis-intermediate-drivers.md)

[NDIS ミニポート ドライバー](ndis-miniport-drivers2.md)

[NDIS プロトコル ドライバー](ndis-protocol-drivers2.md)

 

 






