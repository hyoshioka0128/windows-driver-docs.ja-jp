---
title: ネットワーク データ構造
description: ネットワーク データ構造
ms.assetid: c29aaae6-6f68-404a-90dc-bae005ac9b6e
keywords:
- NET_BUFFER
- NET_BUFFER_LIST
- NET_BUFFER_LIST_CONTEXT
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b78ea7cf518886afdba3899b584325a59b743553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369890"
---
# <a name="network-data-structures"></a>ネットワーク データ構造





ネットワーク経由で送受信データのパケットのネットワーク データで構成されます。 NDIS は、記述し、このようなデータを整理するデータ構造体を提供します。 NDIS 6.0 以降のプライマリ ネットワーク データの構造は次のとおりです。

-   [**NET\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff568376)
-   [**NET\_バッファーの一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)
-   [**NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)

次の図は、これらの構造体間のリレーションシップを示しています。

![図に示す ndis 6.0 ネットワークのデータ構造体](images/netbufferstructures.png)

NDIS 6.0 以降では、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)はネットワーク データをパッケージ化するための基本的な構成要素です。 各ネット\_バッファーの構造体が、MDL チェーン。 データのアドレスは、データをバッファー MDLs マップ領域を NET\_バッファーの構造体を指定します。 このデータ マッピングのと同じですが、MDL チェーンその NDIS 5。*x*で以前のドライバーを使用して、 [ **NDIS\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff557086)構造体。 NDIS は、MDL チェーンを操作する関数を提供します。

複数の NET\_バッファーの構造体は、NET にアタッチできる\_バッファー\_リスト構造体。 NET\_バッファーの構造体が NULL で終わるシングル リンク リストとして構成されています。 NET の発生元のドライバーだけ\_バッファー\_リスト構造体、または NDIS、挿入および削除の NET に直接リンク リストを変更する必要があります\_バッファーの構造体。

[**NET\_バッファー リスト**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体には、すべてを記述する情報が含まれて、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)リストにアタッチされている構造体。 NET に、ドライバーがこのような情報を格納、ドライバーは、コンテキスト情報の追加の領域を必要とする場合\_バッファー\_一覧\_CONTEXT 構造体。 NDIS を割り当て、およびネットワーク内のデータ アクセス機能を提供する\_バッファー\_一覧\_CONTEXT 構造体。

複数の NET\_バッファー\_NET のリストを形成するリストの構造体を接続できる\_バッファー\_リストの構造体。 NET\_バッファー\_リストの構造体が NULL で終わるシングル リンク リストとして構成されています。 ドライバーは、挿入および削除の NET に直接リンク リストを変更できます\_バッファー\_リストの構造体。

## <a name="related-topics"></a>関連トピック


[**NET\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff568376)

[NET\_バッファーの構造体](net-buffer-structure.md)

[**NET\_バッファーの一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[NET\_バッファー\_リスト構造](net-buffer-list-structure.md)

[**NET\_バッファー\_一覧\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff568389)

[NET\_バッファー\_一覧\_CONTEXT 構造体](net-buffer-list-context-structure.md)

 

 






