---
title: NET_BUFFER_LIST ジェネレーション間のリレーションシップ
description: NET_BUFFER_LIST ジェネレーション間のリレーションシップ
ms.assetid: 37b3b08d-4656-47bc-b656-a03f208e4311
keywords:
- NET_BUFFER_LIST
- 親/子 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップ WDK ネットワーク
- WDK NET_BUFFER_LIST のリレーションシップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048ac090b239589ba34dc838e9042efac04e22fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549202"
---
# <a name="relationships-between-netbufferlist-generations"></a>NET 間のリレーションシップ\_バッファー\_一覧の世代





ドライバー作成者が理解し、親 (オリジナル) 間の関係を維持する必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造と (派生)、子構造を複製、フラグメント、および再アセンブリの操作に起因します。

複製/フラグメント/再アセンブリの関数の呼び出し元が子 NET で親ポインターを含む、親/子の関係を維持\_バッファー\_リスト構造と子の数。 子の数により、すべての子が解放された後、呼び出し元が、親を解放します。 次の規則が適用されます。

-   ドライバーは、子から構造を作成した後、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体には、親の構造体の所有権を保持する必要があり、子を渡す必要がありますその他のドライバーを構造体。 ドライバーは、NET の親を渡す必要がありますしない\_バッファー\_を別のドライバーの一覧の構造体。

-   ドライバーは NET の親の子の数を更新する必要がありますのみ\_バッファー\_リスト構造体。 親の構造体は、別のドライバーに渡されることはありません、ために、子の数の値が上書きされることがあるリスクはありません。 ドライバーは、親の構造体を指す子構造体で親ポインターを設定する必要があります。

-   ドライバーが、NET を受信すると\_バッファー\_から別のドライバー、ドライバーの一覧は親ポインターを上書きする必要があります。 場合、受信した NET\_バッファー\_リスト構造は、子、既にその親ポインターを設定する必要があります。 ドライバーは、NET を使用できます\_バッファー\_リストが親構造体として別のドライバーから受け取りました。

-   NDIS では、上記の規則は適用されません。 NET の現在の所有者\_バッファー\_リスト構造は、子の数と親ポインターを管理する必要があります。 たとえば、現在の所有者は複製し、両方、NET のフラグメント\_バッファー\_リスト構造では、親ポインターと子のカウンターが管理する必要があります。

-   カウントを 0 にし、親へのポインター、NDIS 設定、子**NULL** 、NET を割り当てるときに\_バッファー\_リスト構造体。 NDIS は、これらのフィールドのドライバーは、NET を通過するたびを変更しないは\_バッファー\_を別のドライバーの一覧の構造体。

## <a name="related-topics"></a>関連トピック


[NET の派生\_バッファー\_リストの構造体](derived-net-buffer-list-structures.md)

 

 






