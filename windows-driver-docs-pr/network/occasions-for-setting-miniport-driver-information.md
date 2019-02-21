---
title: 場合設定ミニポート ドライバー情報
description: 場合設定ミニポート ドライバー情報
ms.assetid: 46834d76-e1b9-440c-af18-a4b564d1a76e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b0ef7ce7e8709f3171c922bc57fff1fbc6e08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552701"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>場合設定ミニポート ドライバー情報





[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)コネクションレス ミニポート ドライバーで関数と[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)関数で、接続指向のミニポート ドライバーは初期化中に呼び出されます。 これらの関数を呼び出すこともできます。

-   ハードウェアのリセット中

-   プロトコルを呼び出す場合[ **NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)します。

*MiniportOidRequest*または*MiniportCoOidRequest*中に呼び出される[ハードウェア リセット操作](hardware-reset.md)します。 この場合、 *MiniportOidRequest*または*MiniportCoOidRequest*ミニポート ドライバーをそのアドレスに対して初期状態にリセットすると呼びます。

NDIS 呼び出し*MiniportOidRequest*または*MiniportCoOidRequest*プロトコルのミニポート ドライバーの NIC を閉じるときに[ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)呼び出します。 アドレス指定情報を更新するこのようなミニポート ドライバーが要求されます。

 

 





