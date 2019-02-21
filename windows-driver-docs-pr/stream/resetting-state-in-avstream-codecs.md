---
title: AVStream コーデックで状態をリセットします。
description: AVStream コーデックで状態をリセットします。
ms.assetid: c50014fe-bff0-43f4-8552-24e8e97f636b
keywords:
- AVStream ハードウェア コーデック サポート WDK、状態をリセットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffaf707a6a58810d8fe1ef435c3d8e0908d3bc34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529705"
---
# <a name="resetting-state-in-avstream-codecs"></a>AVStream コーデックで状態をリセットします。


MFT を送信するパイプラインのストリーミング メディアをストリーム データを破棄し、ストリーミングの状態をリセット、\_メッセージ\_コマンド\_MFT をフラッシュします。 HW MFT が、MFT を受信すると\_メッセージ\_コマンド\_フラッシュ、MFT 送信[ **IOCTL\_KS\_リセット\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff560832)KSRESET の値を持つ\_入力と出力ピンを開始します。 指定することでリセット通知を受信するミニドライバーがサブスクライブする必要があります、 [ *AVStrMiniPinReset* ](https://msdn.microsoft.com/library/windows/hardware/ff556354)コールバックで、**リセット**のメンバー [ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)します。

ドライバーは、この IOCTL を受信するとをすべての未処理の複製ポインターを削除し、前のすべての内部状態をリセットします。 別の IOCTL 受信後、ドライバーは、保留中の IO 要求がフラッシュ、\_KS\_リセット\_KSRESET の値と状態\_終了します。

この時点では、ミニドライバーは、次のストリームから新しい入力をそのまま使用できるようにする必要があります。

正常に動作する、リセット、ミニドライバーする必要がありますトポロジの接続を指定型の配列を指定することによって、入力と出力ピンの間に注意してください[ **KSTOPOLOGY\_接続**](https://msdn.microsoft.com/library/windows/hardware/ff567148)で**接続**のメンバー、 [ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)構造体。

リセット IOCTL は次のシナリオにも送信されます。 ドライバーが、KSSTREAM を設定するときに\_ヘッダー\_OPTIONSF\_ENDOFSTREAM ストリーム ヘッダー フラグし、ストリーム ポインターをロック解除、KS IOCTL を生成すると、キューをフラッシュする\_KS\_のリセット\_状態の呼び出し KSRESET の値を持つ\_ドライバーに終了します。

このケースで、ドライバーは、要求を開始する前に、せずに終了要求を受信、ドライバーは設定[ **KSPIN**](https://msdn.microsoft.com/library/windows/hardware/ff563483).**ResetState** KSRESET に\_終了します。 この場合は、出力ピンにのみ適用されます。

 

 




