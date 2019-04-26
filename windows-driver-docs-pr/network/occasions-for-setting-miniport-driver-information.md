---
title: ミニポート ドライバー情報の設定の場面
description: ミニポート ドライバー情報の設定の場面
ms.assetid: 46834d76-e1b9-440c-af18-a4b564d1a76e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b0ef7ce7e8709f3171c922bc57fff1fbc6e08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359198"
---
# <a name="occasions-for-setting-miniport-driver-information"></a>ミニポート ドライバー情報の設定の場面





[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)コネクションレス ミニポート ドライバーで関数と[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)関数で、接続指向のミニポート ドライバーは初期化中に呼び出されます。 これらの関数を呼び出すこともできます。

-   ハードウェアのリセット中

-   プロトコルを呼び出す場合[ **NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)します。

*MiniportOidRequest*または*MiniportCoOidRequest*中に呼び出される[ハードウェア リセット操作](hardware-reset.md)します。 この場合、 *MiniportOidRequest*または*MiniportCoOidRequest*ミニポート ドライバーをそのアドレスに対して初期状態にリセットすると呼びます。

NDIS 呼び出し*MiniportOidRequest*または*MiniportCoOidRequest*プロトコルのミニポート ドライバーの NIC を閉じるときに[ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)呼び出します。 アドレス指定情報を更新するこのようなミニポート ドライバーが要求されます。

 

 





