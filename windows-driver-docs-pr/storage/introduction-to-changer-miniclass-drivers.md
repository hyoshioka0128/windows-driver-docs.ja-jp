---
title: チェンジャー ミニクラス ドライバーの概要
description: チェンジャー ミニクラス ドライバーの概要
ms.assetid: ce0f78a3-69ae-4ca7-b2e1-f4892e35a230
keywords:
- チェンジャー ドライバー WDK ストレージ、miniclass ドライバー
- 記憶域チェンジャー ドライバー WDK、miniclass ドライバー
- miniclass ドライバー WDK チェンジャー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5dea73e27243821da5ee8c8de3501b91b33052b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571047"
---
# <a name="introduction-to-changer-miniclass-drivers"></a>チェンジャー ミニクラス ドライバーの概要


## <span id="ddk_introduction_to_changer_miniclass_drivers_kg"></span><span id="DDK_INTRODUCTION_TO_CHANGER_MINICLASS_DRIVERS_KG"></span>


新しいチェンジャーをサポートするには、ドライバー開発者は、システム提供のチェンジャー クラス ドライバーにリンクするチェンジャー miniclass ドライバーを実装します。 チェンジャーをシステムが既に提供しないドライバーをサポートするためだけ新しいチェンジャー miniclass ドライバーを記述する必要があります。

新しい miniclass ドライバーを実装する前を確認してください。

-   デバイスでは、true チェンジャーおよびシリアル アクセス スタッカーではありません。 チェンジャーをスタッカーのように、固定のシーケンスではなく、ランダムな順序は、そのドライブにマウントするメディアを許可します。

-   デバイスのドライブは書き込み-光学ドライブは、ワームなどの CD-R または DVD-R したら

-   デバイスのドライブはすべて、同じ型、CD-ROM や CD-R などの型を混同しません。

Microsoft のオペレーティング システムは書き込みをサポートしていません-1 回の光学式ドライブまたはドライブの 1 つ以上の型とチェンジャーします。

 

 




