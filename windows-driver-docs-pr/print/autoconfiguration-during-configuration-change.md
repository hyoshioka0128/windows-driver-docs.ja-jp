---
title: 構成変更時の自動構成
description: 構成変更時の自動構成
ms.assetid: 0294d34d-06e4-4e57-8f4d-4100ab482852
keywords:
- 構成の変更時の自動構成の WDK プリンター
- 構成の変更時のプリンター自動構成 WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1738f7058a18a03947d0f318e4ace83f01326ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842840"
---
# <a name="autoconfiguration-during-configuration-change"></a>構成変更時の自動構成


デバイスをインストールした後、ポートモニターは、イベントを送信するか、ポーリングすることによって、構成データを最新の状態に保つ役割を担います。 ドライバーまたはアプリケーションがデバイスの現在の構成に関心を持っている場合は常に、 [bidi 通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)と[bidi 通信スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)を使用して、この情報をポートモニターに照会できます。

次の図は、デバイスの構成が変更されたときの自動構成のデータフローを示しています。

![デバイスの構成が変更されたときの自動構成のデータフローを示す図](images/autocfgcfgchange.png)

1.  デバイスの構成が変更されると、Web サービスイベント (WS-ATOMICTRANSACTION) プロトコルを使用するデバイスは、その状態が変更されたことを print サブシステムに通知しますが、特定の変更については説明しません。 標準 TCP/IP ポートモニタは、WS-ADDRESSING をサポートしていないデバイスをポーリングします。

2.  ポートモニタは、デバイスの構成が変更されたことを示す通知を生成し、その通知をスプーラに送信します。

3.  スプーラは、`DrvPrinterEvent` を呼び出してプリンター\_イベント\_構成\_UPDATE を呼び出して、ドライバーに通知を送信します。 この関数呼び出しは、デバイスの構成が変更されたことをドライバーに通知するために機能します。

ドライバーは、デバイスの構成が変更されたタイミングを判断できます。これは、通知メッセージに変更された値が含まれているためです (スキーマは Bidi 通知デザイン仕様で定義されています)。 ただし、通知が大きすぎて通知メカニズムを使用して送信できない場合、通知には1つ以上の ReducedSchema インスタンスが含まれます。各インスタンスは、デバイスの特性が変更されたことを示しますが、新しい値の詳細は含まれません。

 

 




