---
title: シリアル デバイスの割り込みを共有する
description: シリアル デバイスの割り込みを共有する
ms.assetid: 1d35fbc0-7031-42f3-bb22-52d2bcdcfa92
keywords:
- COM ポートの WDK シリアル デバイス
- COM ポート、シリアル デバイス WDK
- 従来の COM ポートの WDK シリアル デバイス
- シリアル デバイスの割り込みを共有
- WDK、割り込みのシリアル デバイス
- 割り込み WDK シリアル デバイス
- 割り込み WDK シリアル デバイスを共有
- シリアル ドライバー WDK、割り込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2005f1fa54d0220b6b999bde1f86691ea50255b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351821"
---
# <a name="sharing-a-serial-device-interrupt"></a>シリアル デバイスの割り込みを共有する





同じマルチポート ボード上の従来の COM ポートは、1 つの割り込みを共有します。 マルチポートのボード上の COM ポートは、インデックス、またはポートを対応するデバイス オブジェクトに関連付けられるマスクによって識別されます。

スタンドアロンのシリアル デバイスは、割り込みを共有することもできます。 ただし、共有の割り込みみ使用 1 つのデバイスで、一度にします。 デバイスが開かれると、シリアル デバイスに割り込みを割り当てます。 デバイスが閉じられたときに、ドライバーは別のデバイスで使用するための割り込みを解放します。

 

 




