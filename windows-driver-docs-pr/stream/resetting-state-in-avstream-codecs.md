---
title: AVStream コーデックの状態のリセット
description: AVStream コーデックの状態のリセット
ms.assetid: c50014fe-bff0-43f4-8552-24e8e97f636b
keywords:
- AVStream ハードウェア コーデック サポート WDK、状態をリセットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 782655c19a115b8b547602364446b2b3715ee655
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383141"
---
# <a name="resetting-state-in-avstream-codecs"></a>AVStream コーデックの状態のリセット


MFT を送信するパイプラインのストリーミング メディアをストリーム データを破棄し、ストリーミングの状態をリセット、\_メッセージ\_コマンド\_MFT をフラッシュします。 HW MFT が、MFT を受信すると\_メッセージ\_コマンド\_フラッシュ、MFT 送信[ **IOCTL\_KS\_リセット\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ni-ks-ioctl_ks_reset_state)KSRESET の値を持つ\_入力と出力ピンを開始します。 指定することでリセット通知を受信するミニドライバーがサブスクライブする必要があります、 [ *AVStrMiniPinReset* ](https://docs.microsoft.com/previous-versions/ff556354(v=vs.85))コールバックで、**リセット**のメンバー [ **KSPIN\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)します。

ドライバーは、この IOCTL を受信するとをすべての未処理の複製ポインターを削除し、前のすべての内部状態をリセットします。 別の IOCTL 受信後、ドライバーは、保留中の IO 要求がフラッシュ、\_KS\_リセット\_KSRESET の値と状態\_終了します。

この時点では、ミニドライバーは、次のストリームから新しい入力をそのまま使用できるようにする必要があります。

正常に動作する、リセット、ミニドライバーする必要がありますトポロジの接続を指定型の配列を指定することによって、入力と出力ピンの間に注意してください[ **KSTOPOLOGY\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection)で**接続**のメンバー、 [ **KSFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)構造体。

リセット IOCTL は次のシナリオにも送信されます。 ドライバーが、KSSTREAM を設定するときに\_ヘッダー\_OPTIONSF\_ENDOFSTREAM ストリーム ヘッダー フラグし、ストリーム ポインターをロック解除、KS IOCTL を生成すると、キューをフラッシュする\_KS\_のリセット\_状態の呼び出し KSRESET の値を持つ\_ドライバーに終了します。

このケースで、ドライバーは、要求を開始する前に、せずに終了要求を受信、ドライバーは設定[ **KSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin).**ResetState** KSRESET に\_終了します。 この場合は、出力ピンにのみ適用されます。

 

 




