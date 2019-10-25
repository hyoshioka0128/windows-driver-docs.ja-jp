---
title: ドライバーのフィルター
description: ドライバーのフィルター
ms.assetid: 626547ba-4c26-4be7-b209-c5e26daf56ab
keywords:
- フィルタードライバー WDK ネットワーク、アーキテクチャ
- NDIS フィルタードライバー WDK、アーキテクチャ
- フィルターモジュール WDK ネットワーク
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7109a28ea32251b2b978997c4ceaf1651472f83e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838895"
---
# <a name="filter-drivers"></a>ドライバーのフィルター

Ndis 6.0 では、NDIS フィルタードライバーが導入されました。 フィルタードライバーは、プロトコルドライバーとミニポートドライバー間の相互作用を監視および変更できます。 フィルタードライバーは実装が簡単で、NDIS 中間ドライバーよりも処理オーバーヘッドが少なくなります。

*フィルターモジュール*は、フィルタードライバーのインスタンスです。 次の図に示すように、通常、フィルターモジュールはミニポートアダプターとプロトコルバインドの間に階層化されています。

![フィルターモジュールを使用した ndis ドライバースタックを示す図](images/filterstack.png)

フィルタードライバーは、ndis ライブラリを通じて NDIS ドライバーとその他の NDIS ドライバーと通信します。 NDIS ライブラリでは、フィルタードライバーが呼び出す必要があるすべてのオペレーティングシステム関数をカプセル化する関数の完全なセット (**NdisF * xxx*** およびその他の**NDIS * xxx*** 関数) がエクスポートされます。 さらに、フィルタードライバーは、NDIS が独自の目的のため、または他のドライバーの代わりに、フィルタードライバーにアクセスするために、一連のエントリポイント (*Filterxxx*関数) をエクスポートする必要があります。

> [!NOTE]
> NDIS ドライバースタックと、4つのすべての NDIS ドライバーの種類の関係を示す図の詳細については、「 [Ndis ドライバースタック](ndis-driver-stack.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

[NDIS フィルタードライバー](ndis-filter-drivers2.md)

[NDIS フィルタードライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)