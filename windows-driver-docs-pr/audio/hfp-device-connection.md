---
title: HFP デバイスの接続
description: HFP デバイス接続のトピックでは、オーディオ システムを決定する方法について説明し、Bluetooth の接続の状態情報をハンドル ハンズフリー プロファイル (HFP) デバイス。
ms.assetid: 29B33A3F-63BB-4E1E-B245-E90372A7812F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 673930dc731aa5cfe7ae575372e6c65feb1eb167
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333541"
---
# <a name="hfp-device-connection"></a>HFP デバイスの接続


HFP デバイス接続のトピックでは、オーディオ システムを決定する方法について説明し、Bluetooth の接続の状態情報をハンドル ハンズフリー プロファイル (HFP) デバイス。

オーディオ ドライバーをサポートする必要があります、オーディオ ドライバーのすべての必要に応じて[ **KSPROPERTY\_ジャック\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)します。 オーディオ ドライバーは、 *IsConnected*フィールド フィルター ファクトリのコンテキストでします。 処理するときに、オーディオ ドライバーはこの値を使用して、 **KSPROPERTY\_ジャック\_説明**プロパティ。

ときに[ **IOCTL\_BTHHFP\_デバイス\_取得\_接続\_状態\_UPDATE** ](https://msdn.microsoft.com/library/windows/hardware/dn265106) 、正常に完了します。オーディオ ドライバー更新し*IsConnected*新しい接続の状態にします。 状態が変更された、オーディオ ドライバーが発生、 [ **KSEVENT\_PINCAPS\_JACKINFOCHANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff537134)イベント、接続状態を再評価するオーディオ システム。 オーディオ ドライバーの別のインスタンスを呼び出して**IOCTL\_BTHHFP\_デバイス\_取得\_接続\_状態\_UPDATE** [次へ] の状態を受信するには変更します。 以前の状態の変更を要求し、保留中、引き続き、この 2 つ目の呼び出しは失敗、オーディオ ドライバーが接続状態が更新されないし、状態の情報を変更する別の要求がなさないつまりがあるかどうか。

説明したよう[カーネル ストリーミングに関する考慮事項](kernel-streaming-considerations.md)、オーディオ ドライバーをサポートする必要があります[ **KSPROPERTY\_ONESHOT\_再接続**](https://msdn.microsoft.com/library/windows/hardware/ff537369)と[**KSPROPERTY\_ONESHOT\_切断**](https://msdn.microsoft.com/library/windows/hardware/hh706181)、これらのプロパティのハンドラーでする必要がありますそれぞれと送信 REQUESTCONNECT と REQUESTDISCONNECT Ioctl、HFP ドライバーにします。 これらの Ioctl が、すぐに完了して、オーディオ ドライバーは、返された結果に応答する準備が完了する必要があります。

ここでは、いくつかその他の Bluetooth のオーディオ デバイス接続関連の要因、オーディオ ドライバー開発者が意識する必要があります。

## <a name="span-idstreamchannelspanspan-idstreamchannelspanspan-idstreamchannelspanstream-channel"></a><span id="Stream_channel"></span><span id="stream_channel"></span><span id="STREAM_CHANNEL"></span>Stream のチャンネル


Stream チャネルは、無線による帯域幅のオーディオ ドライバーの割り当てを表します。 ほとんどの場合、これは、SCO チャネルです。 ただし、SCO チャネルの状態の管理の詳細の一部は HFP ドライバー内に完全処理されます。 これには、例のリモート接続を切断なる可能性があるため、呼び出しのシナリオ、HF が可用性グループへのオーディオの転送を開始します (場所、PC の役割を果たし、AG ここで) が含まれます。

## <a name="span-idaudiofilterpinstatesspanspan-idaudiofilterpinstatesspanspan-idaudiofilterpinstatesspanaudio-filter-pin-states"></a><span id="Audio_filter_pin_states"></span><span id="audio_filter_pin_states"></span><span id="AUDIO_FILTER_PIN_STATES"></span>オーディオ フィルター暗証番号 (pin) の状態


オーディオ ドライバー ハンドラーを実装、KS 暗証番号 (pin) の状態 (AVStrMiniPinSetDeviceState に類似) KS ピンが 2 つです。 SCO ストリーム チャネルは、これらのピンを無線でデータを転送するのいずれかの必要があります。 これらのピンのいずれかの KSSTATE への移行時に\_取得、オーディオ ドライバーに送信することによって、チャネルが表示されます[ **IOCTL\_BTHHFP\_ストリーム\_オープン**](https://msdn.microsoft.com/library/windows/hardware/dn265122)HFP ドライバーにします。 これは非同期の呼び出しであり、完了までに数秒かかります。 オーディオ ドライバーを選択し、タイムアウト メカニズムを実装する必要はありません、IOCTL KSSTATE への移行を完了する前に完了するまで待つか\_取得します。

両方の KS ピンが KSSTATE に移行するタイミング\_、オーディオ ドライバーの送信を停止[ **IOCTL\_BTHHFP\_ストリーム\_閉じる**](https://msdn.microsoft.com/library/windows/hardware/dn265120) HFP ドライバーにします。 これを迅速に完了します。

送信するタイミングを決定する**IOCTL\_BTHHFP\_ストリーム\_オープン**と**IOCTL\_BTHHFP\_ストリーム\_閉じる**、オーディオ ドライバー、SCO ストリーム チャネルを必要とするピンの数を追跡するために、単純な参照カウントのメカニズムを使用できます。 オーディオ ドライバーは、開いてから、参照カウントが 0 から 1 に変更されたときに、SCO ストリーム チャネルを閉じます。

**IOCTL\_BTHHFP\_ストリーム\_開く**HFP ドライバー、SCO チャネルを要求するがない場合は、開くには、および SCO 要求からの結果に要求を完了します。 **IOCTL\_BTHHFP\_ストリーム\_閉じる**HFP ドライバーは、1 つが開いている場合に、SCO チャネル切断を要求します。

## <a name="span-idremotescoconnectanddisconnectspanspan-idremotescoconnectanddisconnectspanspan-idremotescoconnectanddisconnectspanremote-sco-connect-and-disconnect"></a><span id="Remote_SCO_connect_and_disconnect"></span><span id="remote_sco_connect_and_disconnect"></span><span id="REMOTE_SCO_CONNECT_AND_DISCONNECT"></span>リモート SCO 接続し、切断


リモート SCO 切断、Stream チャネルが閉じられた場合、HFP ドライバー何もしません。 Stream チャネルが開かれている場合、HFP ドライバーは再接続タイマーを開始します。 SCO の切断されている状態を Stream のチャネルがまだ開いている場合、タイマーの期限が切れると、ドライバーは SCO チャネルを要求します。 オーディオ データが転送されない無線 SCO が切断されているため、この期間中にオーディオではギャップが存在がするときに注意してください。 HFP ドライバーは、任意の呼び出しを実行して、オーディオ ドライバーに Stream チャネル状態の変更を通知し、SCO 要求が失敗した場合[ **IOCTL\_BTHHFP\_ストリーム\_取得\_状態\_UPDATE**](https://msdn.microsoft.com/library/windows/hardware/dn265121)します。 リモート SCO 切断が HF デバイス要求への転送呼び出しオーディオのオーディオのゲートウェイに通常関連付けられるので、まれで、この必要があります。 オーディオ ドライバー検討これの途中でエラー状態。

この手順では、VoIP アプリケーション CallButtons API から、オーディオ転送コールバックを受信し、正常にストリーミングのエラーが発生するのではなく、HFP エンドポイントでのオーディオのリソースを解放する時間ができます。

SCO をリモートで接続、ドライバーが単に、接続を受け入れる Stream チャネルが開いている場合。 Stream チャネルが閉じられた HFP ドライバーは接続を受け付けも切断タイマーを開始します。 切断タイマー期限が切れたとき、Stream チャネルを閉じたまま SCO がまだ接続されている場合、ドライバー、SCO 接続が解除されます。

この手順では、VoIP アプリケーション CallButtons API から、オーディオ転送コールバックを受信し、途中で拒否または SCO 接続を閉じることがなく、HFP エンドポイントでのオーディオのリソースを確立する時間ができます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論を概説します。](theory-of-operation.md)  



