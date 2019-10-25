---
title: AVStream コーデックの状態のリセット
description: AVStream コーデックの状態のリセット
ms.assetid: c50014fe-bff0-43f4-8552-24e8e97f636b
keywords:
- AVStream ハードウェアコーデックサポート WDK、状態のリセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 939ccc64cbbbd501d09df0e4d035cbe07060263f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844949"
---
# <a name="resetting-state-in-avstream-codecs"></a>AVStream コーデックの状態のリセット


ストリームデータを破棄してストリーミング状態をリセットするために、メディアストリーミングパイプラインは mft\_メッセージ\_コマンド\_を MFT にフラッシュします。 ハードウェア MFT が\_コマンド\_フラッシュを受信したときに、MFT\_メッセージを受信すると、MFT は、入力ピンと出力ピンを開始\_として、値 KSRESET\_を使用して、 [**IOCTL\_KS\_状態のリセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ni-ks-ioctl_ks_reset_state)を送信します。 ミニドライバーは、 [**Kspin\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)の**Reset**メンバーに[*avstrminipinreset*](https://docs.microsoft.com/previous-versions/ff556354(v=vs.85))コールバックを指定することによって、リセット通知を受信するようにサブスクライブする必要があります。

ドライバーは、この IOCTL を受信すると、未処理のすべての複製ポインターを削除し、以前のすべての内部状態をリセットします。 ドライバーは、保留中の IO 要求をフラッシュした後、別の IOCTL\_KS を受信し、値が KSRESET\_END の\_状態にリセット\_ます。

この時点で、ミニドライバーは次のストリームから新しい入力を受け入れる準備ができています。

リセットを正常に動作させるには、ミニドライバーは、Ksk フィルターの**Connections**メンバーに[**Ksto\_po connection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)型の配列を指定して、入力ピンと出力ピンの間のトポロジ接続を指定する必要があることに注意してください[ **\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造体。

次のシナリオでは、リセット IOCTL も送信されます。 ドライバーが KSK ストリーム\_\_ヘッダーを設定すると、ストリームヘッダーにオプション SF\_ENDOFSTREAM フラグが設定され、ストリームポインターがロック解除されます。 KS は、このキューをフラッシュします。これにより、IOCTL\_KS\_の値を持つリセット\_状態呼び出しが生成されます。KSK をドライバーにリセット\_ます。

この場合、先行する begin 要求なしでドライバーが終了要求を受け取ると、ドライバーは[**Kspin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)を設定する必要があります。**Resetstate 出す**を KSK にリセット\_終了します。 このケースは、出力ピンにのみ適用されます。

 

 




