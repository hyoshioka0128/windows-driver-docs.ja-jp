---
title: 中間ドライバー バインド操作
description: 中間ドライバー バインド操作
ms.assetid: 129a744c-d4d4-4741-9812-e76087c585fc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 468ea83f8f68cca1f51d2ef8796fdc82878a58d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844187"
---
# <a name="intermediate-driver-binding-operations"></a>中間ドライバー バインド操作





ミニポートアダプターが使用可能になると、NDIS は、そのミニポートアダプターにバインドできる任意の中間ドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出します。

中間ドライバーは、「[アダプターへのバインド](binding-to-an-adapter.md)」で説明されているプロトコルバインド操作を提供する必要があります。

バインディング時のアクションとしては、バインディングのアダプター固有のコンテキスト領域の割り当てと初期化、任意の仮想ミニポートの初期化、およびアダプターにバインドするための[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)の呼び出しが含まれます。

中間ドライバーでは、各バインドに個別の[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造プールを割り当てる必要はありません。 中間ドライバーは、ドライバーの設計で独自の構造体を割り当てる必要がある場合にのみ、ネットワーク\_バッファー\_リスト構造プールを割り当てる必要があります。 それ以外の場合、ドライバーは他のドライバーから受け取った構造体を渡すことができます。 このようなドライバーでは、送信と受信に対して異なるプールを割り当てる必要があります。

ネットワークデータを割り当てて管理するための要件の詳細については、「[中間ドライバーネットワークデータ管理](intermediate-driver-network-data-management.md)」を参照してください。

 

 





