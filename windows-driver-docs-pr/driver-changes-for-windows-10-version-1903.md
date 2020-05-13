---
title: Windows 10 バージョン1903のドライバー開発の変更点
description: このセクションでは、Windows 10 でのドライバー開発に関する新機能について説明します。
ms.assetid: 90f7754d-be7a-408d-8b89-b173a86c4fa3
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2bf812f56225743325a273081add70758b784adf
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270419"
---
# <a name="whats-new-in-windows-10-version-1903"></a>Windows 10 バージョン1903の新機能

このセクションでは、Windows 10 Version 1903 (Windows 10 April 2019 Update) でのドライバー開発に関する新機能と更新された機能について説明します。

## <a name="audio"></a><a name="audio-1903"></a>オーディオ

Windows 10 Version 1903 の新機能と更新されたオーディオ機能の一覧を次に示します。

* 新しい [eventdetectoroemadapter.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/) ヘッダーの音声ライセンス認証に使用されるオーディオ OEM アダプターに関する新しい参照トピック。
* 新しい Far フィールド オーディオ情報: 
    * [PKEY_Devices_AudioDevice_Microphone_IsFarField](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-devices-audiodevice-microphone-isfarfield)
    * [KSPROPSETID_InterleavedAudio](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-interleavedaudio)
    * [KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION](https://review.docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-interleavedaudio-formatinformation)
    
* [USB オーディオ 2.0 ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/usb-2-0-audio-drivers)の新しいジャックの説明情報。

## <a name="camera"></a><a name="camera-1903"></a>カメラ

Windows 10 Version 1903 で追加された新しいカメラ ドライバーのドキュメントと機能を次に示します。

* 新しい [IR Torch](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-irtorchmode) では、IR カメラの赤外線トーチの電力レベルとデューティ サイクルを設定するプロパティ コントロールを拡張しました。
* 新しい [KSCATEGORY_NETWORK_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-network-camera) デバイス。
* 次のコントロール セレクター用の新規および更新された [USB ビデオ クラス (UVC) 1.5 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)のドキュメント。
  * MSXU_CONTROL_FACE_AUTHENTICATION
  * MSXU_CONTROL_METADATA
  * MSUX_CONTROL_IR_TORCH


## <a name="debugging"></a>デバッグ

Windows 10 バージョン1903のデバッガーには、次のような変更が加えられています。

* Windows オペレーティング システム固有のエラーの種類を追跡しやすいように、新しい停止コードが追加されました。 さらに、いくつかの既存のバグ チェックに関するトピックが拡張および更新されました。 詳細については、「[バグ チェック コード リファレンス](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)」を参照してください。

* 使いやすさを向上させるために KDNET トピックを更新しました。たとえば、新しい「[KDNET ネットワーク カーネル デバッグの自動設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)」です

* IP V6 KDNET のサポートが更新されました。

* 新しい [JavaScript のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting)のトピック

## <a name="display"></a><a name="display-1903"></a>ディスプレイ

Windows 10 Version 1903 では、ディスプレイ ドライバー開発に関する次の更新が行われました。

* **スーパーウェット インク** フロントバッファー レンダリングが可能になる新しい DDI が追加されました。 [D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags) と [PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation) を参照してください。

* **可変レート シェーディング** レンダリングされた画像全体にさまざまなレートのレンダリング パフォーマンス/電力の割り当てが可能になります。 [PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062) と [D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062) を参照してください。

* **診断情報の収集** OS で、レンダリング機能と表示機能の両方で構成されるグラフィックス アダプター用ドライバーからプライベート データを収集できるようになります。 [DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo) を参照してください。

* **バックグラウンド処理** ユーザー モード ドライバーで、目的のスレッド動作と、それを制御または監視するランタイムを表現できるようになります。 ユーザー モード ドライバーでは、バックグラウンド スレッドをスピンアップし、可能な限り低い優先度を割り当てます。また、これらのスレッドによってクリティカル パス スレッドが中断せず、全般的には成功するように NT スケジューラを利用します。 [PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062) を参照してください。

* **ドライバーのホット更新** OS コンポーネントを更新する必要がある場合に、サーバーのダウンタイムを可能な限り短縮します。 [DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate) と [DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate) を参照してください。

## <a name="networking"></a><a name="networking-1903"></a>ネットワーク

## <a name="netadaptercx"></a>NetAdapterCx

NetAdapter WDF クラス拡張機能 (NetAdapterCx) では、ネット リング バッファーはネット リングに置き換えられました。これには、ネット リング反復子を使用してネットワーク データを送受信するための新しいインターフェイスがあります。 新しいトピックの一覧を次に示します。

* [ネット リングの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/introduction-to-net-rings)
* [ネット リングを使用したネットワーク データの送信](https://docs.microsoft.com/windows-hardware/drivers/netcx/sending-network-data-with-net-rings) (およびデータの送信方法を示す新しいアニメーション)
* [ネット リングを使用したネットワーク データの受信](https://docs.microsoft.com/windows-hardware/drivers/netcx/receiving-network-data-with-net-rings) (およびデータの受信方法を示す新しいアニメーション)
* [ネット リングを使用したネットワーク データの取り消し](https://docs.microsoft.com/windows-hardware/drivers/netcx/canceling-network-data-with-net-rings)

この機能をサポートする新しいヘッダーを次に示します。

* [Ring.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/index)
* [Ringcollection.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/ringcollection/index)
* [Netringiterator.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/index)

NetAdapterCx コンテンツの更新の一覧を次に示します。

* 既定のアダプター オブジェクトは、1 つのアダプター オブジェクトの種類のために削除されました。 次のトピックが適宜更新されました。

  * [Summary of NetAdapterCx objects (NetAdapterCx オブジェクトの概要)](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-netadaptercx-objects)
  * [Device and adapter initialization (デバイスとアダプターの初期化)](https://docs.microsoft.com/windows-hardware/drivers/netcx/device-and-adapter-initialization)

* ハードウェア オフロードとパケット拡張 DDI は新しいヘッダーに再編成されました。

  * [Checksum.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksum/index)
  * [Checksumtypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksumtypes/index)
  * [Extension.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/extension/index)
  * [Lso.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/lso/index)
  * [Lsotypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/lsotypes/index)
  * [Rsc.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsc/index)
  * [Rsctypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsctypes/index)

* 基本的なネットワーク データ構造、パケット、およびフラグメントは更新され、新しいヘッダーに組み込まれました。

  * [Packet.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/index)
  * [Fragment.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/fragment/index)

* コールバックのサンプルとパケット キューの主な操作を含めるために、[キューの送信と受信](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues)に関するトピックを見直しました。

## <a name="mobile-operator-scenarios"></a>通信事業者のシナリオ

通信事業者がモバイル プラン アプリを介して Windows 10 デバイス上で顧客にプランを直接販売するための新しいモバイル プラン コンテンツ。

* [モバイル プラン](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/mobile-plans)

## <a name="mobile-broadband"></a><a name="mobilebroadband-1903"></a>モバイル ブロードバンド

Windows 10 Version 1903 のモバイル ブロードバンドに次の機能が追加されました。

* 新しい [SIM カード (UICC) ファイル/アプリケーション システム アクセス](https://docs.microsoft.com/windows-hardware/drivers/network/mb-uicc-application-and-file-system-access)機能
* 新しい[移動体通信時間情報 (NITZ)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-nitz-support) 機能。
* 新しい [DSS によるモデムのログ記録](https://docs.microsoft.com/windows-hardware/drivers/network/mb-modem-logging-with-dss)機能。
* 新しい [5G データ クラスのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-5g-data-class-support)機能。

## <a name="power-management-framework"></a>電源管理フレームワーク

電源管理フレームワーク (PoFx) により、ドライバーは、デバイス内の個々のコンポーネントに対して個別に調整可能なパフォーマンス状態のセットをいくつでも定義することができます。 このドライバーは、パフォーマンスの状態を使ってコンポーネントのワークロードを調整し、現在のニーズに最適なパフォーマンスを提供します。 詳しくは、「[Component-Level Performance State Management (コンポーネント レベルのパフォーマンス状態の管理)](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-performance-management)」をご覧ください。

Windows 10 Version 1903 には [Directed Power Management Framework (DFx)](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-the-directed-power-management-framework) のサポートが含まれています。  以下の関連する参照ドキュメントがあります。

* [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3)
* [PO_FX_DIRECTED_POWER_DOWN_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_down_callback)
* [PO_FX_DIRECTED_POWER_UP_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)
* [PoFxCompleteDirectedPowerDown](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompletedirectedpowerdown) 関数

DFx のテストについては、以下のページを参照してください。

* [有向 FX 単一デバイス テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
* [有向 FX システムの検証テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
* [PwrTest DirectedFx シナリオ](devtest/pwrtest-directedfx-scenario.md)

## <a name="print"></a><a name="print-1903"></a>印刷

Windows 10 Version 1903 で追加された新しい印刷ドライバーのドキュメントと機能を次に示します。

* 新しい USB 印刷 IOCTL:

  * [IOCTL_USBPRINT_GET_INTERFACE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_interface_type)
  * [IOCTL_USBPRINT_GET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_protocol)
  * [IOCTL_USBPRINT_SET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_set_protocol)

* 新しい **fpRegeneratePrintDeviceCapabilities** [PRINTPROVIDER](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_printprovidor) 構造体メンバーと更新されたドキュメント。

## <a name="sensors"></a><a name="sensors-1903"></a>センサー

Windows 10 Version 1903 のセンサー ドライバー開発の新機能には、画面の明るさをテストして調整するための [MALT (Microsoft Ambient Light Tool) ツール](https://docs.microsoft.com/windows-hardware/drivers/sensors/testing-malt-building-a-light-testing-tool)が含まれています。

Ambient Color OEM ホワイトペーパーも更新されました。

## <a name="storage"></a><a name="storage-1903"></a>ストレージ

Windows 10 Version 1903 には次のストレージ機能が追加されました。

* ETW イベントでデバイスの障害とハードウェア プロトコル エラーをログに記録し、プラットフォーム D3 の望ましい動作を照会する新しい Storport API
* ストレージ デバイスまたはアダプターのプロパティを設定するための新しい API
* ファイル システムでは、作成の完了時に拡張属性 (EA) 情報の取得をサポートする新しい DDI が追加され、ミニフィルターで ECP ペイロードを変更して、より高いフィルターを変更できるようになりました

## <a name="windows-driver-frameworks-wdf"></a>Windows Driver Framework (WDF)

Windows 10 Version 1903 の Windows Driver Framework (WDF) には、Kernel-Mode Driver Framework (KMDF) バージョン 1.29 と User-Mode Driver Framework (UMDF) バージョン 2.29 が含まれます。

これらのフレームワーク バージョンに含まれる機能については、「[What's New for WDF Drivers in Windows 10 (Windows 10 の WDF ドライバーの新機能)](https://docs.microsoft.com/windows-hardware/drivers/wdf/)」をご覧ください。
WDF の以前のバージョンで追加された機能については、「[KMDF Version History (KMDF のバージョン履歴)](https://docs.microsoft.com/windows-hardware/drivers/wdf/kmdf-version-history)」と「[UMDF Version History (UMDF のバージョン履歴)](https://docs.microsoft.com/windows-hardware/drivers/wdf/umdf-version-history)」をご覧ください。

## <a name="windows-hardware-error-architecture-whea"></a>Windows Hardware Error Architecture (WHEA)

Windows 10 Version 1903 では、WHEA へのインターフェイスが簡単になりました。  詳細については、次のページを参照してください。

* [**WheaAddErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
* [**WheaReportHwErrorDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
* [**WheaRemoveErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
* [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
* [*WHEA_ERROR_SOURCE_READY_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_ready_device_driver)
* [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
* [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

## <a name="wi-fi"></a><a name="wifi-1903"></a>Wi-Fi

新しい Wi-Fi ドライバーの開発ドキュメントと機能を次に示します。

* 新しい Fine Timing Measurement (FTM) 機能
* 新しい [WPA3-SAE 認証](https://docs.microsoft.com/windows-hardware/drivers/network/wpa3-sae-authentication)機能
* エンタープライズ シナリオでローミング パフォーマンスを向上させるための新しい Multiband Operation (MBO) のサポート
* 新しいビーコン レポート オフロードのサポート
* これらの新機能に関する OID コマンド、NDIS の状態表示、および TLV については、「[WDI ドキュメントの変更履歴](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-doc-change-history)」を参照してください。

次のトピックは、Windows 10 Version 1903 に合わせて更新されました。

* [WDI_AUTH_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm) - WPA3-SAE 認証のサポートが追加されました
* [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame) と [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-response-action-frame) - 送信ポイント ツー ポイント (P2P) アクション フレームの新しい検証が追加されました