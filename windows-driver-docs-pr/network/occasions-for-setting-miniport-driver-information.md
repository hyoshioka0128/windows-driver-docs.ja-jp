---
title: ミニポート ドライバー情報の設定の場面
description: ミニポート ドライバー情報の設定の場面
ms.assetid: 46834d76-e1b9-440c-af18-a4b564d1a76e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab733cf4cb30b9e25ecb8a13e77f6a4c7adad042
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368508"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>ミニポート ドライバー情報の設定の場面





[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)コネクションレス ミニポート ドライバーで関数と[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)関数で、接続指向のミニポート ドライバーは初期化中に呼び出されます。 これらの関数を呼び出すこともできます。

-   ハードウェアのリセット中

-   プロトコルを呼び出す場合[ **NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)します。

*MiniportOidRequest*または*MiniportCoOidRequest*中に呼び出される[ハードウェア リセット操作](hardware-reset.md)します。 この場合、 *MiniportOidRequest*または*MiniportCoOidRequest*ミニポート ドライバーをそのアドレスに対して初期状態にリセットすると呼びます。

NDIS 呼び出し*MiniportOidRequest*または*MiniportCoOidRequest*プロトコルのミニポート ドライバーの NIC を閉じるときに[ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)呼び出します。 アドレス指定情報を更新するこのようなミニポート ドライバーが要求されます。

 

 





