---
title: HFP デバイスの接続
description: HFP デバイス接続のトピックでは、オーディオシステムが Bluetooth ハンズフリープロファイル (HFP) デバイスの接続状態情報を決定および処理する方法について説明します。
ms.assetid: 29B33A3F-63BB-4E1E-B245-E90372A7812F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2feea23c231598f93d69b8c8f2d384e4be31139d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831188"
---
# <a name="hfp-device-connection"></a>HFP デバイスの接続


HFP デバイス接続のトピックでは、オーディオシステムが Bluetooth ハンズフリープロファイル (HFP) デバイスの接続状態情報を決定および処理する方法について説明します。

すべてのオーディオドライバーに必要な場合は、オーディオドライバーが[**Ksk プロパティ\_ジャック\_の説明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)をサポートしている必要があります。 オーディオドライバーは、フィルターファクトリコンテキストに*IsConnected*フィールドを保持します。 この値は、 **Ksk プロパティ\_ジャック\_DESCRIPTION**プロパティを処理するときに、オーディオドライバーによって使用されます。

[**IOCTL\_BTHHFP\_デバイス\_\_接続を取得し\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update)を正常に完了すると、オーディオドライバーは新しい接続状態で*IsConnected*を更新します。 状態が変化した場合、オーディオドライバーは[**KSEVENT\_PINCAPS\_JACKINFOCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-jackinfochange)イベントを発生させ、オーディオシステムが接続状態を再評価します。 次に、オーディオドライバーは、 **BTHHFP\_\_デバイス\_** の別の IOCTL インスタンスを呼び出して、\_接続\_状態\_更新を取得して次の状態の変更を受信します。 まだ保留中の状態の変更要求がある場合、この2回目の呼び出しは失敗し、オーディオドライバーは接続状態を更新せず、状態の変更に関する別の要求を行いません。

「[カーネルストリーミングに関する考慮事項](kernel-streaming-considerations.md)」で説明されているように、オーディオドライバーは[**KSK プロパティ\_ONESHOT\_RECONNECT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-oneshot-reconnect)および[**KSPROPERTY\_ONESHOT\_切断**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-oneshot-disconnect)をサポートする必要があります。これらのプロパティのハンドラーは、REQUESTCONNECT と REQUESTCONNECT の Ioctl をそれぞれ HFP ドライバーに送信します。 これらの Ioctl は迅速に完了します。オーディオドライバーは、返された結果に応答する準備ができている必要があります。

オーディオドライバーの開発者が知っておく必要があるその他の Bluetooth オーディオデバイス接続関連の要因を次に示します。

## <a name="span-idstream_channelspanspan-idstream_channelspanspan-idstream_channelspanstream-channel"></a><span id="Stream_channel"></span><span id="stream_channel"></span><span id="STREAM_CHANNEL"></span>ストリームチャネル


ストリームチャネルは、オーディオドライバーによる無線帯域幅の割り当てを表します。 ほとんどの場合、これは SCO チャネルです。 ただし、SCO チャネルの状態の管理の詳細については、HFP ドライバー内で完全に処理されます。 これには、たとえば、HF が AG へのオーディオ転送を開始する (このケースでは、PC が AG の役割を果たす) 呼び出しシナリオが原因であるリモート切断の例が含まれます。

## <a name="span-idaudio_filter_pin_statesspanspan-idaudio_filter_pin_statesspanspan-idaudio_filter_pin_statesspanaudio-filter-pin-states"></a><span id="Audio_filter_pin_states"></span><span id="audio_filter_pin_states"></span><span id="AUDIO_FILTER_PIN_STATES"></span>オーディオフィルターの pin の状態


オーディオドライバーは、2つの KS ピンの KS ピン状態ハンドラー (AVStrMiniPinSetDeviceState に似ています) を実装しています。 これらのいずれかのピンが無線経由でデータを転送するには、SCO ストリームチャネルが必要です。 これらのいずれかのピンが KSK 状態に遷移すると\_取得されます。そのため、オーディオドライバーは、HFP ドライバーに対して開いている[**IOCTL\_BTHHFP\_\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open)を送信することによってチャネルを開きます。 これは非同期呼び出しであり、完了するまでに数秒かかることがあります。 オーディオドライバーは、独自のタイムアウトメカニズムを実装する必要はなく、IOCTL が完了するまで待機してから、KSSTATE\_の取得への移行を完了する必要があります。

両方の KS ピンが KSK 状態に移行すると\_停止すると、オーディオドライバーは[**BTHHFP\_\_ストリームの\_IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close)を hfp ドライバーの近くに送信します。 これは短時間で完了します。

**Bthhfp\_ストリーム\_オープン**および**ioctl\_bthhfp\_ストリーム**を\_送信するタイミングを決定するために、オーディオドライバーは単純な参照カウントメカニズムを使用して、の pin の数を追跡できます。SCO ストリームチャネルが必要です。 参照カウントが0から1に変更されると、オーディオドライバーは SCO ストリームチャネルを開いて閉じます。

**IOCTL\_BTHHFP\_ストリーム\_開い**ている場合、hfp ドライバーは sco チャネル (まだ開いていない場合) を要求し、sco 要求の結果を使用して要求を完了します。 **IOCTL\_BTHHFP\_ストリーム\_** hfp ドライバーが開いている場合は、SCO チャネルの切断を要求します。

## <a name="span-idremote_sco_connect_and_disconnectspanspan-idremote_sco_connect_and_disconnectspanspan-idremote_sco_connect_and_disconnectspanremote-sco-connect-and-disconnect"></a><span id="Remote_SCO_connect_and_disconnect"></span><span id="remote_sco_connect_and_disconnect"></span><span id="REMOTE_SCO_CONNECT_AND_DISCONNECT"></span>リモート SCO 接続と切断


リモート SCO 切断では、ストリームチャネルが閉じている場合、HFP ドライバーは何も行いません。 ストリームチャネルが開かれている場合、HFP ドライバーは再接続タイマーを開始します。 タイマーの有効期限が切れた場合、SCO がまだ切断されていて、ストリームチャネルが開いたままになっていると、ドライバーは SCO チャネルを要求します。 SCO が切断されている間は、電波を介したオーディオデータ転送が行われないので、この期間中はオーディオに差が生じます。 SCO 要求が失敗した場合、HFP ドライバーは、呼び出し中の[**IOCTL\_BTHHFP\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)を完了することによって、ストリームチャネルの状態の変更をオーディオドライバーに通知します。これにより\_状態\_更新プログラムが取得され\_ます。 リモートの SCO 切断は通常、オーディオゲートウェイへの呼び出しオーディオの転送を要求する HF デバイスに関連付けられているため、この方法はめったに発生しません。 オーディオドライバーは、これをストリームストリームのエラー状態と見なす必要があります。

この手順によって、VoIP アプリケーションが CallButtons API からオーディオ転送コールバックを受信し、そのオーディオリソースを HFP エンドポイントでクリーンに解放する時間が発生します。ストリーミングエラーは発生しません。

リモート SCO 接続では、ストリームチャネルが開いている場合、ドライバーは単に接続を受け入れます。 ストリームチャネルが閉じている場合、HFP ドライバーは接続を受け入れ、切断タイマーも開始します。 切断タイマーの有効期限が切れた場合、SCO がまだ接続されていて、ストリームチャネルがまだ閉じていると、ドライバーは SCO 接続を解除します。

この手順では、VoIP アプリケーションが CallButtons API からオーディオ転送コールバックを受信し、HFP エンドポイントでオーディオリソースを確立するまでの時間を指定します。これにより、SCO 接続を早めに拒否したり閉じたりする必要がなくなります。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論](theory-of-operation.md)  



