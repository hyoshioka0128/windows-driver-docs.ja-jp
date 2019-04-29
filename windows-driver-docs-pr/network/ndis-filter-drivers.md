---
title: フィルター ドライバー
description: フィルター ドライバー
ms.assetid: 626547ba-4c26-4be7-b209-c5e26daf56ab
keywords:
- フィルター ドライバー WDK ネットワー キング、アーキテクチャ
- NDIS フィルター ドライバー WDK、アーキテクチャ
- フィルター モジュールの WDK ネットワーク
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: bf4f4afd2decbf012cad359eb60173d5e3c5298d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392929"
---
# <a name="filter-drivers"></a>フィルター ドライバー

NDIS 6.0 には、NDIS フィルター ドライバーが導入されました。 フィルター ドライバーは、監視し、プロトコルおよびミニポートのドライバーの間の相互作用を変更できます。 フィルター ドライバーを実装し、以下の処理オーバーヘッド NDIS 中間ドライバよりも簡単です。

A*フィルター モジュール*フィルター ドライバーのインスタンスです。 次の図に示すように、フィルター モジュールが通常ミニポート アダプターとプロトコルのバインドの間で階層化します。

![フィルター モジュールでの ndis ドライバー スタックを示す図](images/filterstack.png)

フィルター ドライバーは、NDIS ライブラリからドライバーを NDIS およびその他の NDIS と通信します。 NDIS ライブラリ関数の完全なセットをエクスポートします (**NdisF * Xxx*** およびその他の**Ndis * Xxx*** 関数) をカプセル化するすべてのフィルター ドライバーを呼び出す必要のあるオペレーティング システム関数。 フィルター ドライバーではさらに、エントリ ポイントのセットをエクスポートする必要があります (*FilterXxx*関数) その NDIS は、独自の目的で、またはフィルター ドライバーにアクセスするその他のドライバーの代わりを呼び出します。

> [!NOTE]
> NDIS ドライバー スタックと 4 つすべての NDIS ドライバーの種類間のリレーションシップを示す図の詳細については、次を参照してください。 [NDIS ドライバー スタック](ndis-driver-stack.md)します。

## <a name="related-topics"></a>関連トピック

[NDIS フィルター ドライバー](ndis-filter-drivers2.md)

[NDIS フィルター ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff565527)