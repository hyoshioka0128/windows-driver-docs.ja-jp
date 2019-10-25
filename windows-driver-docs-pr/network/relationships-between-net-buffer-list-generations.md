---
title: NET_BUFFER_LIST 世代間の関係
description: NET_BUFFER_LIST 世代間の関係
ms.assetid: 37b3b08d-4656-47bc-b656-a03f208e4311
keywords:
- NET_BUFFER_LIST
- 親/子 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- リレーションシップ (WDK NET_BUFFER_LIST)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 466b01723c7007bfc85f504c7eed65fa9f8bcd02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842062"
---
# <a name="relationships-between-net_buffer_list-generations"></a>NET\_BUFFER\_LIST Generation のリレーションシップ





ドライバーの作成者は、親 (元) の[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造と、複製、フラグメント、および再アセンブル操作の結果として得られる子 (派生) 構造との間の関係を理解し、維持する必要があります。

複製/フラグメント/再構築関数の呼び出し元は、親子関係を維持します。これには、子ネット\_バッファー\_リスト構造の親ポインターと子の数が含まれます。 子の数は、すべての子が解放された後に、呼び出し元が親を解放することを保証します。 次の規則が適用されます。

-   ドライバーは、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体から子構造を作成した後、親構造の所有権を保持し、子構造体を他のドライバーに渡す必要があります。 ドライバーは、親の NET\_BUFFER\_LIST 構造体を別のドライバーに渡すことはできません。

-   ドライバーは、親の NET\_BUFFER\_LIST 構造内の子の数のみを更新する必要があります。 親の構造は別のドライバーに渡されないため、子の数の値が上書きされる危険性はありません。 ドライバーは、親構造体を指すように子構造体の親ポインターを設定する必要があります。

-   ドライバーが別のドライバーから NET\_BUFFER\_LIST を受け取ると、ドライバーは親ポインターを上書きしないようにする必要があります。 受信した NET\_BUFFER\_LIST 構造体が子である場合は、その親ポインターが既に設定されている必要があります。 ドライバーは、別のドライバーから受信した NET\_BUFFER\_リストを親構造として使用できます。

-   NDIS では、上記の規則は適用されません。 NET\_BUFFER\_LIST 構造体の現在の所有者は、子の数と親のポインターを管理する必要があります。 たとえば、現在の所有者が NET\_BUFFER\_LIST 構造体の複製とフラグメント化を行う場合、親ポインターと子カウンターを管理する必要があります。

-   NDIS は、子の数をゼロに設定し、親ポインターが NET\_BUFFER\_LIST 構造体を割り当てるときに**NULL を返し**ます。 NDIS では、ドライバーが NET\_BUFFER\_LIST 構造体を別のドライバーに渡すたびに、これらのフィールドが変更されることはありません。

## <a name="related-topics"></a>関連トピック


[派生 NET\_BUFFER\_LIST 構造体](derived-net-buffer-list-structures.md)

 

 






