---
title: オブジェクト ハンドルとイベントの順序
description: オブジェクト ハンドルとイベントの順序
ms.assetid: 5abbcda2-66cc-4460-99b6-e7796e65af68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5ecfa4de9f6cdf0670d56d197662a0ab8a32497
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379656"
---
# <a name="object-handle-and-event-order"></a>オブジェクト ハンドルとイベントの順序





Microsoft PTP WIA ミニドライバーを発行したとき、 **GetObjectHandles**コマンド (ピマ 15740 標準を参照)、カメラが正しく、WIA 項目のツリーを構築する WIA ミニドライバーの特定の順序でオブジェクト ハンドルを返す必要があります。

-   子オブジェクトのオブジェクトは、その子の前に一覧に表示する必要があります。

    ハンドルの数値の順序は重要ではありません。 たとえば、オブジェクト 5 4、6、および 7、子オブジェクトがある場合、リスト注文 5、4、6、7。 4、5、6、順序付け 7 は機能しません。

-   補助的な関連付けは、アソシエーションの他のオブジェクトの前のオブジェクト ハンドルの一覧で、イメージ オブジェクトを配置する必要があります。

-   ボトムアップ式の順序では、(ピマ 15740 標準を参照してください) ObjectRemoved イベントが発生する必要があります。

    つまり、ObjectRemoved イベントの結果としてそのすべての子が削除されるまでオブジェクトの ObjectRemoved イベントは発生しません。 補助的なアソシエーション内のイメージを削除する場合は、イメージ自体が削除される前に、ObjectRemoved イベントに応答アソシエーションの他のオブジェクトを削除する必要があります。

 

 




