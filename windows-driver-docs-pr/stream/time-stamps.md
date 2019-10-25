---
title: タイム スタンプ
description: タイム スタンプ
ms.assetid: a97a57df-294a-4cbb-85d3-56d33ece65c9
keywords:
- ビデオキャプチャ WDK AVStream、タイムスタンプ
- ビデオのキャプチャ WDK AVStream、タイムスタンプ
- WDK ビデオキャプチャのタイムスタンプ
- 時計 WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9abfc3262db97431b542cab383aa718d40138899
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845545"
---
# <a name="time-stamps"></a>タイム スタンプ


ミニドライバーは、複数のデータストリームを同期するために、データパケットをタイムスタンプする必要があります。 カーネルモードクロックは、最初に**Ksk 状態\_停止**状態から移行した時間のカウントを開始します。 その後、クロックは、ストリームが**Ksk 状態\_停止**状態に遷移するまでの間隔で、100ナノ秒単位の一定の間隔でタイムスタンプをインクリメントする必要があります。

転送される各データパケットは、1つのフレームまたはビデオまたは補助的なデータのフィールドに対応します。 フレーム精度のビデオキャプチャに関係するビデオキャプチャドライバーライターは、他のすべてのフィルターが参照として使用できるクロックを提供するように選択できます。 Digital video ミニドライバーは、フィルターグラフで使用する時計を提供するミニドライバーの例です。 また、USB や IEEE 1394 の会議カメラなど、他のマルチメディアストリームに対して非同期に実行されるビデオキャプチャミニドライバーは、オーディオデジタイザーなどの別のコンポーネントによって提供されるクロックでデータパケットをスタンプする必要があります。

ストリームクラスミニドライバーがマスタークロックを提供する場合は、 [**HW\_ストリーム\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)構造体で次の値を指定する必要があります。

```cpp
PHW_STREAM_OBJECT *pStreamObject;
 
PStreamObject->HWClockFunction = (PHW_CLOCK_FUNCTION)StreamClockRoutine;
PStreamObject->ClockSupportFlags = CLOCK_SUPPORT_CAN_READ_ONBOARD_CLOCK | CLOCK_SUPPORT_CAN_RETURN_STREAM_TIME;
```

 

 




