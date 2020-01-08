---
title: チェンジャー Miniclass ドライバーについて
description: チェンジャー Miniclass ドライバーについて
ms.assetid: ce0f78a3-69ae-4ca7-b2e1-f4892e35a230
keywords:
- チェンジャードライバー WDK storage、miniclass drivers
- storage チェンジャードライバー WDK、miniclass ドライバー
- miniclass drivers WDK チェンジャー
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 290eef3135d095147fc5e2d27e3f8331a186eea6
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606562"
---
# <a name="about-changer-miniclass-drivers"></a>チェンジャー Miniclass ドライバーについて

新しいチェンジャーをサポートするために、ドライバーライターは、システム指定のチェンジャークラスドライバーにリンクするチェンジャー miniclass ドライバーを実装します。 新しいチェンジャー miniclass ドライバーは、システムによってドライバーがまだ提供されていないチェンジャーをサポートするためにのみ書き込まれる必要があります。

新しい miniclass ドライバーの実装を開始する前に、次のことを確認する必要があります。

- デバイスは、シリアルアクセススタッカーではなく、真のチェンジャーです。 チェンジャーは、スタッカーのように、固定シーケンスではなく、ランダムな順序でメディアをドライブにマウントすることを許可します。

- デバイスのドライブには、WORM、CD-R、DVD-R など、ライトワンスの光学ドライブは書き込まれません。

- デバイスのドライブはすべて同じ種類であり、CD-ROM や CD-R などの種類が混在しているわけではありません。

Microsoft オペレーティングシステムでは、複数の種類のドライブを持つ書き込み1回の光学ドライブまたはチェンジャーはサポートされていません。
