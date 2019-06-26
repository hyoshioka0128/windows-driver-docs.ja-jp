---
title: タイム スタンプ
description: タイム スタンプ
ms.assetid: a97a57df-294a-4cbb-85d3-56d33ece65c9
keywords:
- ビデオ キャプチャ WDK AVStream、タイムスタンプ
- ビデオの WDK AVStream、タイムスタンプのキャプチャ
- タイム スタンプ WDK のビデオのキャプチャ
- クロックの WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 509b0a1b4879e0edb8474a971d8b2f0bdf20f801
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377742"
---
# <a name="time-stamps"></a>タイム スタンプ


ミニドライバーは、複数のデータ ストリームを同期するスタンプ データ パケットを時間必要があります。 カーネル モードの時計が時間のうち最初に移行するタイミングのカウントを開始、 **KSSTATE\_停止**状態。 その後、クロックがインクリメント タイムスタンプ 100 ナノ秒単位の定期的な間隔でするストリームの遷移まで、 **KSSTATE\_停止**状態。

転送されるデータ パケットは、1 つのフレームまたはビデオまたは補助的なデータのフィールドに対応します。 クロックの参照として使用できるその他のすべてのフィルターを提供するビデオの正確なフレームのキャプチャと懸念を抱いているビデオ キャプチャ ドライバー開発者が選択できます。 デジタル ビデオ ミニドライバーは、フィルターのグラフで使用するクロックを提供するミニドライバーの例です。 または、ビデオ キャプチャ ミニドライバー USB および IEEE 1394 の会議用カメラなどの他のマルチ メディア ストリームを非同期的に実行する時間をスタンプのクロックを使用して、データ パケットがオーディオのデジタイザーなどの別のコンポーネントによって提供される必要があります。

次の値を指定する必要があります、Stream クラス ミニドライバーでは、マスターのクロックを提供する場合、 [ **HW\_ストリーム\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_object)構造体。

```cpp
PHW_STREAM_OBJECT *pStreamObject;
 
PStreamObject->HWClockFunction = (PHW_CLOCK_FUNCTION)StreamClockRoutine;
PStreamObject->ClockSupportFlags = CLOCK_SUPPORT_CAN_READ_ONBOARD_CLOCK | CLOCK_SUPPORT_CAN_RETURN_STREAM_TIME;
```

 

 




