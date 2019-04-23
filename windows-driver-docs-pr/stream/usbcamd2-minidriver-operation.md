---
title: USBCAMD2 ミニドライバーの操作
description: USBCAMD2 ミニドライバーの操作
ms.assetid: 395612cd-3407-4b42-b3a5-0afa838e73d9
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 ミニドライバーの操作
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
- される Srb WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f94f562f0c91c5d50fe3eb2847fa7a9717637bd
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903732"
---
# <a name="usbcamd2-minidriver-operation"></a>USBCAMD2 ミニドライバーの操作

USBCAMD2 カメラのミニドライバーは、一般には、次のように動作します。

- カメラのミニドライバー呼び出し[ **USBCAMD\_DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_driverentry)からその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 ミニドライバーを呼び出すと**USBCAMD\_DriverEntry**、ミニドライバーの USBCAMD2 に渡す[ **AdapterReceivePacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine)コールバック関数。 USBCAMD2 のミニドライバーを登録し、 *stream.sys*クラス ドライバー。

- カメラ ミニドライバーでさまざまなストリーム要求のブロック (される Srb) を受信できますし、その*AdapterReceivePacket*などを処理するコールバック関数。
  - [**SRB\_初期化\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialize-device)
  - [**SRB\_初期化\_完了**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialization-complete)
  - [**SRB\_GET\_STREAM\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)
  - [**SRB\_取得\_デバイス\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)
  - [**SRB\_設定\_デバイス\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)
  - [**SRB\_取得\_データ\_積集合**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection)
  - [**SRB\_OPEN\_STREAM**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)
- カメラのミニドライバーは、各 SRB を処理する必要がある方法を決定します。 ミニドライバーは、処理される Srb の推進のために、USBCAMD2 ミニドライバー ライブラリ ルーチンを呼び出すことができます。 これらのルーチンは、通常で始まる、 *USBCAMD\_* プレフィックス。

たとえば、カメラ ミニドライバー カメラ ミニドライバーの USBCAMD2 の別のコールバック関数を指定するには、指定のエントリ ポイントを[ **USBCAMD\_デバイス\_DATA2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_usbcamd_device_data2)構造体。 ミニドライバーを呼び出して[ **USBCAMD\_InitializeNewInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)渡す初期化 USBCAMD\_デバイス\_USBCAMD2 DATA2 構造体。 USBCAMD2 は、必要な場合に、ミニドライバーのコールバック関数を呼び出します。

> [!NOTE]
> [ **USBCAMD\_デバイス\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_usbcamd_device_data)の旧バージョンと互換性の目的でのみ USBCAMD2 で構造体がサポートされています。

呼び出す必要があります、ミニドライバー [ **USBCAMD\_AdapterReceivePacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket) USBCAMD2 を処理するにハンドルされない任意される Srb を送信します。

[**USBCAMD ライブラリのコールバック関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/index#callback-functions)ミニドライバーを実装するコールバック関数と省略可能または必須いるかどうかについて説明します。

次の手順の一覧は、カメラ ミニドライバーに送信される Srb の処理の一般的なフローを示しています。

## <a name="minidrivers-srbinitializedevice-handler"></a>ミニドライバーの SRB\_初期化\_デバイス ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | USBCAMD2 を呼び出すことによって初期化[ **USBCAMD_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)ビデオを示す、または、まだデバイス イベントの有効化などのカーネル モードで生の処理の要件。 |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | USB デバイスと構成記述子を取得します。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamConfigureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)コールバック関数。 |
| カメラのミニドライバー | 構成を完了します。 代替の設定と最大転送サイズを選択します。 配列を入力[ **USBCAMD_Pipe_Config_Descriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)構造体。 |
| USBCAMD2 | 配列を解析**USBCAMD_Pipe_Config_Descriptor**構造体。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_initialize_routine)コールバック関数。 |
| カメラのミニドライバー | 初期化を完了します。 デバイスの電源を設定し、カメラの既定の設定をアクティブ化します。 |
| USBCAMD2 | ストリームおよびストリーム記述子サイズの数を指定、 **stream.sys**クラス ドライバー。 |

## <a name="minidrivers-srbgetstreaminfo-handler"></a>ミニドライバーの SRB\_取得\_ストリーム\_情報ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 提供、 [ **HW_STREAM_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)ストリーム情報構造体、 **stream.sys**クラス ドライバー。 |
| カメラのミニドライバー | デバイスのプロパティ セット内の配列へのポインターの塗りつぶし**stream.sys**クラス ドライバーの[ **HW_STREAM_HEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)構造体。 |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | ストリーム ヘッダー内のピンの数を入力します。 |
| USBCAMD2 | 存在する場合は、デバイスのイベント テーブルを公開します。 |
| USBCAMD2 | ストリーム情報のテーブルでは、エントリの値を修正します。 設定カテゴリの名前 (キャプチャまたはも)。 |
| USBCAMD2 | ストリーム プロパティ配列へのポインターを入力します。 |

## <a name="minidrivers-srbinitializationcomplete-handler"></a>ミニドライバーの SRB\_初期化\_完了ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | IRP_MJ_PNP と IRP_MN_QUERY_INTERFACE を使用して USBCAMD2 の GUID_USBCAMD_INTERFACE を取得します。 |

## <a name="minidrivers-srbgetdeviceproperty-handler"></a>ミニドライバーの SRB\_取得\_デバイス\_プロパティ ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | カメラのミニドライバーを処理するなどのプロパティを取得[ **PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)、 [ **PROPSETID_VIDCAP_CAMERACONTROL** ](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)、および[ **PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)などその他のカスタム プロパティを設定します。 |

## <a name="minidrivers-srbsetdeviceproperty-handler"></a>ミニドライバーの SRB\_設定\_デバイス\_プロパティ ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | カメラのミニドライバーの処理のパラメーターを取得することによって、プロパティを設定[ **PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)、 [ **PROPSETID_VIDCAP_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)、および[ **PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)、およびカスタム プロパティを設定します。 |

## <a name="minidrivers-srbgetdataintersection-handler"></a>ミニドライバーの SRB\_取得\_データ\_交差ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 返す、 [ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)から構造体、 [ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions//ff561658(v=vs.85))構造体。 |
| カメラのミニドライバー | フレーム レートが要求されたことを確認する (**VideoInfoHeader.AvgTimePerFrame**) が要求されるビデオ形式の上限と下限の範囲内で。 制限を超えた場合、ミニドライバー必要があります ->-> pSrb で次の値が正しい CommandData.IntersectInfo Datarange:VideoInfoHeader.AvgTimePerFrame、VideoInfoHeader.dwBitRate します。 |

## <a name="minidrivers-srbopenstream-handler"></a>ミニドライバーの SRB\_オープン\_ストリーム ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | ビデオ形式を確認します。 |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | カメラのミニドライバーで受け入れられるビデオ形式を保存します。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamAllocateBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_allocate_bw_routine_ex)ビデオ形式のデータに基づく帯域幅の割り当てし、ビデオ形式の最大バッファー サイズを取得するコールバック関数。 |
| カメラのミニドライバー | 要求されたフレーム レートと出力の windows のサイズに適合するアイソクロナス チャネルの最大パケット サイズを計算します。 |
| カメラのミニドライバー | 最も近い別の設定を呼び出すことによって選択[ **USBCAMD_SelectAlternateInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_selectalternateinterface)します。 ミニドライバーは、カメラによって生成できる最大フレーム サイズを USBCAMD2 を提供する必要があります。 |
| カメラのミニドライバー | ハードウェアのカメラのスケーリングを設定します。 場合、レジストリに保存されている値または既定の設定に、カメラ コントロールを設定、初めてです。 |
| カメラのミニドライバー | ビデオの形式の制限内でフレーム レート (VideoInfoHeader.AvgTimePerFrame) があることを確認し、そうでない場合に修正します。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamStartCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex)コールバック関数。 |
| カメラのミニドライバー | ハードウェアのキャプチャ モードを設定します。 |
| USBCAMD2 | アイソクロナスまたは一括転送を初期化します。 |

## <a name="minidrivers-srbclosestream-handler"></a>ミニドライバーの SRB\_閉じる\_ストリーム ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | 保留中の Irp USBCAMD2 に送信をキャンセルします。 保留中のデータのされる Srb を返す、 **stream.sys**クラス ドライバー。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)コールバック関数。 |
| カメラのミニドライバー | カメラに停止キャプチャ コマンドを送信します。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamFreeBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)アイソクロナスを解放するコールバック関数バスの帯域幅、該当する場合。 |
| カメラのミニドライバー | アイドル状態の代替設定を選択します。 |
| USBCAMD2 | USB パイプに関連付けられているリソースを解放します。 |

## <a name="minidrivers-srbuninitializedevice-handler"></a>ミニドライバーの SRB\_非\_デバイス ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | 任意のストリームが開いている場合は、呼び出すようにミニドライバーのして閉じます[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)と[ **CamFreeBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)コールバック各ストリームの機能です。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamUnInitialize** ](https://docs.microsoft.com/previous-versions//ff557646(v=vs.85))コールバック関数。 |
| カメラのミニドライバー | リソースを解放してクリーンアップします。 |

## <a name="minidrivers-srbsurpriseremoval-handler"></a>ミニドライバーの SRB\_突然\_削除ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | 保留中のデータのされる Srb をキャンセルし、STATUS_CANCELLED とされる Srb を返します。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)と[ **CamFreeBandwidthEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)すべての開いているストリームにコールバック関数。 |
| USBCAMD2 | 上の読み書きされる Srb の後に続く SRB_SURPRISE_REMOVAL STATUS_CANCELLED を返します。 |

## <a name="minidrivers-srbsetdataformat-handler"></a>ミニドライバーの SRB\_設定\_データ\_形式ハンドラー

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 新しいビデオ形式を確認します。 |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_SetVideoFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pfnusbcamd_setvideoformat)します。 |
| USBCAMD2 | 関連付けられているストリームの拡張子を持つ新しい形式を保存します。 |

## <a name="minidrivers-srbchangepowerstate-from-power-on-to-power-off-handler"></a>ミニドライバーの SRB\_変更\_POWER\_電源をオンから電源オフ ハンドラーへの状態

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | 該当する場合、アイソクロナス パイプでストリーミングを停止または保留中の一括または割り込みの転送をキャンセルします。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)コールバック関数。 |
| カメラのミニドライバー | ハードウェアにキャプチャの停止コマンドを送信します。 |

## <a name="minidrivers-srbchangepowerstate-from-power-off-to-power-on-handler"></a>ミニドライバーの SRB\_変更\_POWER\_ハンドラーの電源をオンから電源オフ状態

| Component | アクション |
| --- | --- |
| カメラのミニドライバー | 呼び出す[ **USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)します。 |
| USBCAMD2 | 該当する場合、アイソクロナス パイプでストリーミングを再開または一括を再送信または USB クラスへの転送を中断します。 |
| カメラのミニドライバー | カメラの設定とカメラの電力消費量を通常のレベルに復元します。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamStopCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)コールバック関数。 |
| USBCAMD2 | 呼び出すようにミニドライバーの[ **CamStartCaptureEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex)コールバック関数。 |
