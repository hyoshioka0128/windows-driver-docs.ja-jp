---
title: USB 802.3 デバイス サンプル
description: USB 802.3 デバイス サンプル
ms.assetid: 647dd493-a7f4-469a-ab2f-f58f9916333d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 117bbb3b51f40664a27c3b2580f679c82a299a5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380144"
---
# <a name="usb-8023-device-sample"></a>USB 802.3 デバイス サンプル





USB のリモートの NDIS イーサネット デバイスの記述子のサンプル セットを次に示します。 CDC 通信クラス インターフェイスと CDC データ クラス インターフェイスが含まれています。 デバイス記述子が個別に返されるとします。 構成記述子と次のすべての記述子が示されている順序で 1 つのブロックとして返されます。

コントロール メッセージは、コントロール エンドポイントに送信されます。 通知メッセージは、CDC 通信クラス インターフェイスの割り込みのエンドポイントに送信されます。 データのメッセージは、一括でとを一括でエンドポイント CDC データ クラス インターフェイスでします。 文字列記述子は表示されません。

リモートの NDIS 実装は、Windows Millennium Edition では、通信クラス インターフェイスのデータ クラス インターフェイスの前に、前提としています。 ベンダーには、この記述子のデバイスは、Windows Millennium Edition で正しく初期化されるように順序付けを選択する必要があります。

このサンプルの一部が制御する仕様を満たしていない、仕様に準拠します。

 

 





