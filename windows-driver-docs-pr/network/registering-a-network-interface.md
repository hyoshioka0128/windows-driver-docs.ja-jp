---
title: ネットワーク インターフェイスの登録
description: ネットワーク インターフェイスの登録
ms.assetid: 7e3c3b0f-2013-4133-8b52-fa9e66f963cb
keywords:
- NDIS ネットワーク インターフェイス、WDK を登録します。
- ネットワーク インターフェイス、WDK を登録します。
- ネットワーク インターフェイスを登録します。
- NdisIfRegisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13ef1ce1d39472e2714f2d5aac9bbba17575f1f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353299"
---
# <a name="registering-a-network-interface"></a>ネットワーク インターフェイスの登録





コンピューターが再起動されるたびに NDIS 登録されているネットワーク インターフェイスの空のリストから始まります。 インターフェイス プロバイダーを呼び出し、 [ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)関数を開始またはインターフェイスが検出されるたびに、その[ **NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値を認識します。 開始またはインターフェイスを検出するためのメカニズムは、アプリケーション固有です。

**NdisIfRegisterInterface**返します NDIS\_状態\_NDIS では、コンピューター上の既知のインターフェイスの一覧に、指定したインターフェイスを正常に追加する場合にのみ成功します。 この場合、 **NdisIfRegisterInterface**インターフェイス インデックスを返します、 *pIfIndex*パラメーター。 ただしへの呼び出し**NdisIfRegisterInterface**わけでは、インターフェイスはアクティブです。、インターフェイスが存在する、この呼び出しがのみが保証されます。 **NdisIfRegisterInterface**返します NDIS\_状態\_リソース NDIS にインターフェイスを登録するための十分なリソースがない場合。 **NdisIfRegisterInterface**他 NDIS 状態の値を返すこともできます。

*ProviderIfContext*パラメーターの**NdisIfRegisterInterface**ハンドルが含まれています。 このハンドルを、呼び出し元の OID のクエリに渡されると set 関数 - インターフェイスの呼び出し元のコンテキストの領域にします。 *PIfInfo*パラメーターにはへのポインターが含まれています、 [ **NET\_場合\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_if_information)インターフェイスに関する情報を含む構造体。

以下のトピックの詳細については、ネットワークはインターフェイスを**NdisIfRegisterInterface**正常に登録します。

[インターフェイス インデックスの割り当てください。](allocating-an-interface-index.md)

[ネットワーク インターフェイスの情報](network-interface-information.md)

 

 





