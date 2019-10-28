---
title: NET_LUID インデックスの使用
description: NET_LUID インデックスの使用
ms.assetid: 21e0a73b-a02c-4ab4-b7c2-efcb8bfc806d
keywords:
- NDIS ネットワークインターフェイス WDK、NET_LUID
- ネットワークインターフェイス WDK、NET_LUID
- NET_LUID
- インデックス操作の WDK ネットワークインターフェイス
- ローカル一意識別子 WDK ネットワークインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12ee658713e52918ffb996c01e74e3066ffa287f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842995"
---
# <a name="using-a-net_luid-index"></a>NET\_LUID インデックスの使用





NDIS には、NET\_LUID 値を作成するために必要な[**net\_luid**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)インデックスを割り当てて解放する機能が用意されています。 NDIS インターフェイスプロバイダーは、インターフェイスを登録するために、NET\_LUID 値を割り当てる必要があります。

NET\_LUID インデックスを割り当てるには、インターフェイスプロバイダーは[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)関数を呼び出します。 インデックスを割り当てた後、インターフェイスプロバイダーは、net\_LUID 値を構築するために[ **\_net\_luid**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-net-luid)マクロを作成するために、NDIS\_呼び出します。 NET\_LUID インデックスを解放するために、インターフェイスプロバイダーは[**NdisIfFreeNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex)関数を呼び出します。

**NdisIfAllocateNetLuidIndex**は、呼び出し元が*iftype*パラメーターで指定したインターフェイス型に関連付けられている、24ビット値を割り当てようとします。これは、ローカルコンピューターに対して一意です。 インデックス割り当てが成功した場合、 **NdisIfAllocateNetLuidIndex**は NDIS\_STATUS\_SUCCESS を返し、 *Pnetluidindex*パラメーターに指定されているアドレスに NET\_LUID インデックスを提供します。 NDIS が無料の NET\_LUID インデックスを見つけることができない場合、 **NdisIfAllocateNetLuidIndex**は NDIS\_STATUS\_リソースを返します。 **NdisIfAllocateNetLuidIndex**は、ndis 内の内部エラーを示すために他の ndis ステータス値を返すことができます。 NDIS は、後でコンピューターを再起動するときに、このインデックスの割り当てを記録します。 NDIS では、コンピューターの再起動後でも、そのインデックスに割り当てられたインターフェイスプロバイダーがそのインデックスの**NdisIfFreeNetLuidIndex**関数を呼び出すまで、特定のインデックスを使用しません。

[**NdisIfFreeNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex)は、以前に割り当てられた[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)インデックスを解放して、NDIS がそのインデックスを別のインターフェイスに再割り当てできる可能性があります。 呼び出し元は、 [**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)を呼び出して NET\_LUID インデックスを割り当てるときに、呼び出し元が使用する*iftype*で同じインターフェイス型を渡す必要があります。 解放操作が成功した場合、 **NdisIfFreeNetLuidIndex**は NDIS\_STATUS\_SUCCESS を返します。 **NdisIfFreeNetLuidIndex**の呼び出しが失敗した場合、インターフェイスプロバイダーは、NET\_LUID インデックスに関連付けられている永続的なストレージに保存されたすべての情報を削除する必要があります。 情報を削除すると、すべてのコンピューターの再起動後に既に解放されているインデックスをプロバイダーが解放しようとすることがなくなります。 **NdisIfFreeNetLuidIndex**を呼び出した後、呼び出し元は、同じインターフェイス型に対して**NdisIfAllocateNetLuidIndex**を再度呼び出し、解放された同じ NET\_luid インデックスを受け取るまで、NET\_LUID 値を再度使用することはできません。

ネットワークインターフェイスを登録するには、インターフェイスプロバイダーが有効な NET\_LUID 値を[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数に渡す必要があります。 ネットワークインターフェイスの登録の詳細については、「[ネットワークインターフェイスの登録](registering-a-network-interface.md)」を参照してください。

 

 





