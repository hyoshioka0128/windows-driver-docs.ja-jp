---
title: USBCAMD2 ミニドライバーの操作
description: USBCAMD2 ミニドライバーの操作
ms.assetid: 395612cd-3407-4b42-b3a5-0afa838e73d9
keywords:
- Windows 2000 カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- ストリーミングモデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバーライブラリ
- カーネルストリーミングモデル WDK、USBCAMD2 ミニドライバーライブラリ
- USBCAMD2 ミニドライバー operations WDK Windows 2000 カーネルストリーミング
- USB ベースのストリーミングカメラの WDK USBCAMD2
- カメラ WDK USBCAMD2
- SRBs WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80698d295af72b65c4e948de2d61b0c7180e2ad4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845635"
---
# <a name="usbcamd2-minidriver-operation"></a>USBCAMD2 ミニドライバーの操作

通常、USBCAMD2 カメラミニドライバーは次のように動作します。

- カメラミニドライバーは、 [**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから[**USBCAMD\_driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_driverentry)を呼び出します。 ミニドライバーが**USBCAMD\_DriverEntry**を呼び出すと、ミニドライバーの[**adapterreceivepacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-padapter_receive_packet_routine) callback 関数を USBCAMD2 に渡します。 USBCAMD2 は、ミニドライバーを *.sys*クラスドライバーに登録します。

- カメラミニドライバーは、次のように、*アダプターの Adapterreceivepacket*コールバック関数でさまざまなストリーム要求ブロック (SRBs) を受け取ることができます。
  - [**SRB\_\_デバイスの初期化**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialize-device)
  - [**SRB\_の初期化\_完了**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-initialization-complete)
  - [**SRB\_\_ストリーム\_情報の取得**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-stream-info)
  - [**SRB\_GET\_DEVICE\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)
  - [**SRB\_\_デバイス\_プロパティの設定**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)
  - [**SRB\_\_データ\_共通部分を取得する**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-data-intersection)
  - [**SRB\_開いている\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-stream)
- カメラミニドライバーは、各 SRB をどのように処理する必要があるかを決定します。 ミニドライバーは USBCAMD2 ミニドライバーライブラリのルーチンを呼び出して、SRBs の処理を支援することができます。 これらのルーチンは、通常、 *USBCAMD\_* プレフィックスで始まります。

たとえば、カメラミニドライバーのその他のコールバック関数を USBCAMD2 で指定する場合、カメラミニドライバーは[**USBCAMD\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_usbcamd_device_data2)のエントリポイントを指定します。 次に、ミニドライバーは[**USBCAMD\_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)を呼び出して、初期化された USBCAMD\_DEVICE\_DATA2 構造体を USBCAMD2 に渡します。 USBCAMD2 は、必要に応じて、ミニドライバーのコールバック関数を呼び出します。

> [!NOTE]
> [**USBCAMD\_デバイス\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_usbcamd_device_data)構造は、旧バージョンとの互換性のためだけに USBCAMD2 でサポートされています。

ミニドライバーは、 [**USBCAMD\_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出して、USBCAMD2 に対して処理されない SRBs を処理する必要があります。

[**USBCAMD ライブラリのコールバック関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/index#callback-functions)は、ミニドライバーが実装するコールバック関数、および省略可能か必須かを示します。

次の手順の一覧は、カメラミニドライバーに送信される SRBs の処理の一般的な流れを示しています。

## <a name="minidrivers-srb_initialize_device-handler"></a>ミニドライバーの SRB\_INITIALIZE\_デバイスハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**USBCAMD_InitializeNewInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_initializenewinterface)を呼び出すことによって、USBCAMD2 を初期化します。これは、デバイスイベントの有効化など、カーネルモードでのビデオまたは未処理の処理要件を示します。 |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | USB デバイスと構成記述子を取得します。 |
| USBCAMD2 | ミニドライバーの[**CamConfigureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex) callback 関数を呼び出します。 |
| カメラミニドライバー | 構成を完了します。 別の設定と最大転送サイズを選択します。 [**USBCAMD_Pipe_Config_Descriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)構造体の配列を入力します。 |
| USBCAMD2 | **USBCAMD_Pipe_Config_Descriptor**構造体の配列を解析します。 |
| USBCAMD2 | ミニドライバーの[**CamInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_initialize_routine) callback 関数を呼び出します。 |
| カメラミニドライバー | 初期化を完了します。 デバイスの電源を設定し、カメラの既定の設定をアクティブにします。 |
| USBCAMD2 | ストリームの数とストリーム記述子のサイズを、 **.sys**クラスドライバーに指定します。 |

## <a name="minidrivers-srb_get_stream_info-handler"></a>ミニドライバーの SRB\_GET\_ストリーム\_情報ハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**HW_STREAM_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)ストリーム情報の構造体を、 **.sys**クラスドライバーに提供します。 |
| カメラミニドライバー | **Stream. sys**クラスドライバーの[**HW_STREAM_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)構造のデバイスプロパティセットの配列へのポインターを入力します。 |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | ストリームヘッダーの pin の数を入力します。 |
| USBCAMD2 | デバイスイベントテーブルを公開します (存在する場合)。 |
| USBCAMD2 | ストリーム情報テーブルのエントリ値を修正します。 カテゴリ名を設定します (capture またはそれでも)。 |
| USBCAMD2 | ストリームプロパティの配列へのポインターを設定します。 |

## <a name="minidrivers-srb_initialization_complete-handler"></a>ミニドライバーの SRB\_初期化\_完全なハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | IRP_MJ_PNP と IRP_MN_QUERY_INTERFACE を使用して USBCAMD2 の GUID_USBCAMD_INTERFACE を取得します。 |

## <a name="minidrivers-srb_get_device_property-handler"></a>ミニドライバーの SRB\_GET\_DEVICE\_プロパティハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)、 [**PROPSETID_VIDCAP_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)、 [**PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)などのカスタムプロパティセットだけでなく、カメラミニドライバーが処理するプロパティを取得します。 |

## <a name="minidrivers-srb_set_device_property-handler"></a>ミニドライバーの SRB\_SET\_デバイス\_プロパティハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**PROPSETID_VIDCAP_VIDEOPROCAMP**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)、 [**PROPSETID_VIDCAP_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)、 [**PROPSETID_VIDCAP_VIDEOCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocontrol)、およびその他のカスタムプロパティセットのパラメーターを取得することによって、カメラミニドライバーハンドルのプロパティを設定します。 |

## <a name="minidrivers-srb_get_data_intersection-handler"></a>ミニドライバーの SRB\_\_データ\_共通部分ハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**Ksdatarange**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体から、構造体を返します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) |
| カメラミニドライバー | 要求されたビデオ形式の上限と下限の範囲内にあることを確認します (**AvgTimePerFrame**)。 制限を超えている場合、ミニドライバーは pSrb >-IntersectInfo-> Datarange の値を修正する必要があります。-AvgTimePerFrame、VideoInfoHeader. dwBitRate レート。 |

## <a name="minidrivers-srb_open_stream-handler"></a>ミニドライバーの SRB\_OPEN\_ストリームハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | ビデオ形式を確認します。 |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | カメラミニドライバーで受け入れられるビデオ形式を保存します。 |
| USBCAMD2 | ビデオ形式のデータに基づいて帯域幅を割り当て、ビデオ形式の最大バッファーサイズを取得するには、ミニドライバーの[**CamAllocateBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_allocate_bw_routine_ex) callback 関数を呼び出します。 |
| カメラミニドライバー | 要求されたフレームレートと出力ウィンドウサイズを満たす、アイソクロナスチャネルの最大パケットサイズを計算します。 |
| カメラミニドライバー | [**USBCAMD_SelectAlternateInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_selectalternateinterface)を呼び出して、最も近い代替設定を選択します。 ミニドライバーは、カメラによって生成される可能性のある最大フレームサイズを USBCAMD2 に提供する必要があります。 |
| カメラミニドライバー | カメラのハードウェアのスケーリングを設定します。 カメラコントロールをレジストリの格納されている値に設定するか、初めての場合は既定の設定に設定します。 |
| カメラミニドライバー | フレームレート (AvgTimePerFrame) がビデオ形式の制限内に収まっていることを確認し、そうでない場合は修正します。 |
| USBCAMD2 | ミニドライバーの[**CamStartCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex) callback 関数を呼び出します。 |
| カメラミニドライバー | ハードウェアをキャプチャモードに設定します。 |
| USBCAMD2 | アイソクロナスまたは一括転送を初期化します。 |

## <a name="minidrivers-srb_close_stream-handler"></a>ミニドライバーの SRB\_CLOSE\_ストリームハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | USBCAMD2 に送信された保留中の Irp を取り消します。 すべての保留中のデータ SRBs を、 **.sys**クラスドライバーに返します。 |
| USBCAMD2 | ミニドライバーの[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) callback 関数を呼び出します。 |
| カメラミニドライバー | カメラに停止キャプチャコマンドを送信します。 |
| USBCAMD2 | ミニドライバーの[**CamFreeBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex) callback 関数を呼び出して、必要に応じて、アイソクロナスバス帯域幅を解放します。 |
| カメラミニドライバー | アイドル状態の代替設定を選択します。 |
| USBCAMD2 | USB パイプに関連付けられている無料のリソース。 |

## <a name="minidrivers-srb_uninitialize_device-handler"></a>ミニドライバーの SRB\_初期化解除\_デバイスハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | まだ開いているストリームがある場合は、各ストリームに対してミニドライバーの[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)関数と[**CamFreeBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex) callback 関数を呼び出して閉じます。 |
| USBCAMD2 | ミニドライバーの[**CamUnInitialize**](https://docs.microsoft.com/previous-versions/ff557646(v=vs.85)) callback 関数を呼び出します。 |
| カメラミニドライバー | リソースをクリーンアップして解放します。 |

## <a name="minidrivers-srb_surprise_removal-handler"></a>ミニドライバーの SRB\_驚か\_削除ハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | Pending data SRBs をキャンセルし、STATUS_CANCELLED で SRBs を返します。 |
| USBCAMD2 | 開いているすべてのストリームで、ミニドライバーの[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex)関数と[**CamFreeBandwidthEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_free_bw_routine_ex)コールバック関数を呼び出します。 |
| USBCAMD2 | SRB_SURPRISE_REMOVAL 後に停止した読み取り/書き込み SRBs の STATUS_CANCELLED を返します。 |

## <a name="minidrivers-srb_set_data_format-handler"></a>ミニドライバーの SRB\_SET\_データ\_形式ハンドラー

| Component | アクション |
| --- | --- |
| カメラミニドライバー | 新しいビデオ形式を確認します。 |
| カメラミニドライバー | [**USBCAMD_SetVideoFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pfnusbcamd_setvideoformat)を呼び出します。 |
| USBCAMD2 | 新しい形式を、関連付けられたストリーム拡張と共に保存します。 |

## <a name="minidrivers-srb_change_power_state-from-power-on-to-power-off-handler"></a>ミニドライバーの SRB\_電源オンから電源オフハンドラーへの電源\_の状態の\_変更

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | 必要に応じて、アイソクロナスパイプでのストリーミングを停止するか、保留中の一括転送または割り込み転送をキャンセルします。 |
| USBCAMD2 | ミニドライバーの[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) callback 関数を呼び出します。 |
| カメラミニドライバー | キャプチャの停止コマンドをハードウェアに送信します。 |

## <a name="minidrivers-srb_change_power_state-from-power-off-to-power-on-handler"></a>ミニドライバーの SRB は、電源\_の状態を電源オフから電源オンハンドラーに変更\_\_します。

| Component | アクション |
| --- | --- |
| カメラミニドライバー | [**USBCAMD_AdapterReceivePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nf-usbcamdi-usbcamd_adapterreceivepacket)を呼び出します。 |
| USBCAMD2 | 必要に応じて、アイソクロナスパイプでストリーミングを再開するか、または USB クラスに一括または割り込み転送を再送信します。 |
| カメラミニドライバー | カメラの設定とカメラの電力消費を通常のレベルに復元します。 |
| USBCAMD2 | ミニドライバーの[**CamStopCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_stop_capture_routine_ex) callback 関数を呼び出します。 |
| USBCAMD2 | ミニドライバーの[**CamStartCaptureEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_start_capture_routine_ex) callback 関数を呼び出します。 |
