---
title: ネットワーク インターフェイスの登録
description: ネットワーク インターフェイスの登録
ms.assetid: 7e3c3b0f-2013-4133-8b52-fa9e66f963cb
keywords:
- NDIS ネットワークインターフェイス WDK、登録
- ネットワークインターフェイス WDK、登録
- ネットワークインターフェイスの登録
- NdisIfRegisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb710df30599f88697498b6214ee7538d1cb1a09
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842098"
---
# <a name="registering-a-network-interface"></a>ネットワーク インターフェイスの登録





コンピューターが再起動するたびに、NDIS は登録されているネットワークインターフェイスの空の一覧から開始します。 インターフェイスプロバイダーは、インターフェイスを開始または検出するたびに[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数を呼び出し、その[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値が既知であることを確認します。 インターフェイスを開始または検出するメカニズムは、アプリケーション固有です。

**NdisIfRegisterInterface**は、指定されたインターフェイスをコンピューター上の既知のインターフェイスの一覧に正常に追加した場合にのみ、NDIS\_STATUS\_SUCCESS を返します。 この場合、 **NdisIfRegisterInterface**は、 *pifindex*パラメーターでインターフェイスインデックスを返します。 ただし、 **NdisIfRegisterInterface**の呼び出しは、インターフェイスがアクティブであることを意味するわけではありません。この呼び出しは、インターフェイスが存在することだけを保証します。 NDIS にインターフェイスを登録するために使用できる十分なリソースがない場合、 **NdisIfRegisterInterface**は NDIS\_STATUS\_リソースを返します。 **NdisIfRegisterInterface**は、他の NDIS 状態の値も返すことができます。

**NdisIfRegisterInterface**の*ProviderIfContext*パラメーターには、インターフェイスの呼び出し元のコンテキスト領域へのハンドルが含まれています。このハンドルは、呼び出し元の OID クエリおよびセット関数に渡されます。 *PIfInfo*パラメーターには、インターフェイスに関する情報を含む情報の構造を[ **\_場合に、NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_if_information)へのポインターが含まれています。

次のトピックでは、 **NdisIfRegisterInterface**によって正常に登録されるネットワークインターフェイスの詳細について説明します。

[インターフェイスインデックスの割り当て](allocating-an-interface-index.md)

[ネットワークインターフェイスの情報](network-interface-information.md)

 

 





