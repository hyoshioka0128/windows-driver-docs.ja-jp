---
title: NET_LUID インデックスの使用
description: NET_LUID インデックスの使用
ms.assetid: 21e0a73b-a02c-4ab4-b7c2-efcb8bfc806d
keywords:
- NDIS ネットワーク インターフェイス、WDK NET_LUID
- ネットワーク インターフェイス、WDK NET_LUID
- NET_LUID
- インデックス操作の WDK のネットワーク インターフェイス
- WDK ネットワーク インターフェイスのローカル一意識別子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a0cabd3b8de4ffe4dea357b3f56ace763c8874f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360753"
---
# <a name="using-a-netluid-index"></a>NET を使用して\_LUID インデックス





NDIS の割り当てし、解放する機能を提供する、 [ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh) NET の作成に必要なインデックス\_LUID 値。 NET を割り当てる必要があります、NDIS インターフェイス プロバイダー\_インターフェイスを登録する LUID 値。

割り当てる、NET\_LUID インデックス、インターフェイス プロバイダーを呼び出し、 [ **NdisIfAllocateNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifallocatenetluidindex)関数。 インターフェイス プロバイダーを呼び出し、インデックスを割り当てたら、 [ **NDIS\_ように\_NET\_LUID** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-net-luid)ネットを構築するマクロ\_LUID 値。 解放、NET\_LUID インデックス、インターフェイス プロバイダーを呼び出し、 [ **NdisIfFreeNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiffreenetluidindex)関数。

**NdisIfAllocateNetLuidIndex**で呼び出し元が指定されているインターフェイス型に関連付けられている 24 ビットの値を割り当てようとする、 *IfType*パラメーターは、ローカル コンピューターに固有です。 インデックスの割り当てが成功すると、 **NdisIfAllocateNetLuidIndex** NDIS を返します\_状態\_成功し、NET を提供します\_LUID インデックスで提供されているアドレスで、  *。pNetLuidIndex*パラメーター。 NDIS が無料 NET を検索できないかどうか\_LUID インデックス、 **NdisIfAllocateNetLuidIndex**返します NDIS\_状態\_リソース。 **NdisIfAllocateNetLuidIndex** NDIS 内で内部エラーを示す他の NDIS 状態の値を返すことができます。 NDIS は、その後、コンピューターが再起動したときのこのインデックスの割り当てを記録します。 NDIS には使用されません特定のインデックス、今後の呼び出し元コンピューターの再起動後もそのインデックスに割り当てられているインターフェイス プロバイダーを呼び出すまで、 **NdisIfFreeNetLuidIndex**関数のインデックス。

[**NdisIfFreeNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiffreenetluidindex)以前に割り当てられた解放[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh) NDIS に別のインターフェイスには、そのインデックスが再割り当てできます可能性がありますようにインデックスを作成します。 呼び出し元がで同一のインターフェイス型で渡す必要があります*IfType*呼び出されたときに、呼び出し元が使用[ **NdisIfAllocateNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifallocatenetluidindex)ネットを割り当てる\_LUID のインデックス。 無料の操作が成功すると、 **NdisIfFreeNetLuidIndex** NDIS を返します\_状態\_成功します。 場合に呼び出し**NdisIfFreeNetLuidIndex**失敗した場合、インターフェイス プロバイダーは、NET に関連する永続的ストレージに保存されているすべての情報を削除する必要があります\_LUID のインデックス。 情報を削除するには、プロバイダーがすべてのコンピューターを再起動した後は、既に解放されているインデックスを解放して保持はいない保証されます。 呼び出した後**NdisIfFreeNetLuidIndex**、呼び出し元は、NET を使用する必要があります\_LUID の値を呼び出す場合を除き、もう一度**NdisIfAllocateNetLuidIndex**同種インターフェイス用にもう一度受け取ると、同じ NET\_LUID が解放されることをインデックスします。

ネットワーク インターフェイスに登録するインターフェイスをプロバイダーが有効な NET を渡す必要があります\_LUID の値を[ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)関数。 ネットワーク インターフェイスの登録の詳細については、次を参照してください。[ネットワーク インターフェイスを登録する](registering-a-network-interface.md)します。

 

 





