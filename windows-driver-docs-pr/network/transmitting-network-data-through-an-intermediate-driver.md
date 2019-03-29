---
title: 中間ドライバー経由のネットワーク データの転送
description: 中間ドライバー経由のネットワーク データの転送
ms.assetid: 90759322-810b-47fd-896c-465c96be4cdd
keywords:
- 中間ドライバー WDK ネットワーク、データの送信
- NDIS 中間ドライバー WDK、データの送信
- ネットワーク データを送信
- WDK NDIS 中間のデータを転送します。
- WDK NDIS 中間のデータを転送します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d82c2602edf324facab2918faf05ff0444cb87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580147"
---
# <a name="transmitting-network-data-through-an-intermediate-driver"></a>中間ドライバー経由のネットワーク データの転送





説明したよう[ミニポート ドライバーとして中間のドライバーを登録する](registering-an-intermediate-driver-as-a-miniport-driver.md)、中間のドライバーを提供する必要があります、 [ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)関数と、登録[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。 *MiniportSendNetBufferLists*関数は、着信を転送できる[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)呼び出して構造[**NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)場合、ドライバーはコネクションレスの下端。 *MiniportSendNetBufferLists* NET の一覧を送信できる\_バッファー\_リストの構造体を受け取る**NdisSendNetBufferLists**基になるミニポートの機能に関係なくドライバー。

*MiniportSendNetBufferLists* NET の一覧を受信\_バッファー\_リストの構造体の後続の呼び出し元によって定義された順序で配置された**NdisSendNetBufferLists**します。 ほとんどの場合、中間のドライバーが保持この順序 NET の受信の配列が渡されます\_バッファー\_基になるミニポート ドライバーにリストの構造体。 基になるドライバーに渡す前に、ネットワーク データでデータを変更する中間のドライバーでは、一覧を並べ替えることができます。

NDIS の順序を常に維持[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ポインターへのリンク リストとして渡された構造体**NdisSendNetBufferLists**. 基になるミニポート ドライバーは、そのリストに渡されるも想定しています。 その*MiniportSendNetBufferLists*関数では、同じ順序でネットワーク データを送信する必要があることを意味します。

 

 





