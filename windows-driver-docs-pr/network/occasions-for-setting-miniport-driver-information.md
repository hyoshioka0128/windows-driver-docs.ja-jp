---
title: ミニポート ドライバー情報の設定の場面
description: ミニポート ドライバー情報の設定の場面
ms.assetid: 46834d76-e1b9-440c-af18-a4b564d1a76e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 577b0f667b328acd120966f9d4647cb6f84b14ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842166"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>ミニポート ドライバー情報の設定の場面





コネクションレスミニポートドライバーの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数と接続指向ミニポートドライバーの[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)関数は、初期化中に呼び出されます。 これらの関数は、次のように呼び出すこともできます。

-   ハードウェアのリセット中に、

-   プロトコルが[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)を呼び出す場合。

*Miniportoidrequest*または*MiniportCoOidRequest*は、[ハードウェアのリセット操作](hardware-reset.md)中に呼び出されます。 この場合、 *Miniportoidrequest*または*MiniportCoOidRequest*が呼び出され、ミニポートドライバーがそのアドレスに対して初期状態にリセットされます。

ミニポートドライバーの NIC がプロトコルの[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)呼び出しによって閉じられた場合、NDIS は*Miniportoidrequest*または*MiniportCoOidRequest*を呼び出します。 このようなミニポートドライバーは、アドレス指定情報を更新するように要求されます。

 

 





