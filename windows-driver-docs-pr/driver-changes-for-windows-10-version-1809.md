---
title: Windows 10 バージョン1809のドライバー開発の変更点
description: このセクションでは、Windows 10 でのドライバー開発に関する新機能について説明します。
ms.assetid: 764bcd98-c123-45e2-9dd1-44d54bb1addc
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: ebc1e1b963d05c79707011bcff981b6b650444f9
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270417"
---
# <a name="whats-new-in-windows-10-version-1809"></a>Windows 10 Version 1809 の最新情報

このセクションでは、Windows 10 Version 1809 (Windows 10 October 2018 Update) でのドライバー開発に関する新機能と更新された機能について説明します。

## <a name="audio"></a><a name="audio-1809"></a>オーディオ

新しい [sidebandaudio](https://docs.microsoft.com/windows-hardware/drivers/ddi/sidebandaudio/) ヘッダーと [usbsidebandaudio](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbsidebandaudio/) ヘッダーに関するドキュメントが公開されました。

## <a name="bluetooth"></a><a name="bluetooth-1809"></a>Bluetooth

* HCI_VS_MSFT_Read_Supported_Features が更新され、セキュリティで保護されたシンプルなペアリング プロセスのための新しいフラグが追加されました。 「[Microsoft-defined Bluetooth HCI commands and events (Microsoft が定義した Bluetooth HCI のコマンドとイベント)](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/microsoft-defined-bluetooth-hci-commands-and-events#hcivsmsftreadsupportedfeatures)」をご覧ください。

* Windows 10 Version 1809 の新しい QDID はこちら([108589](https://launchstudio.bluetooth.com/ListingDetails/55701)) で確認できます。 すべてのリリースの全 QD ID の一覧については、「[Bluetooth](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)」をご覧ください。

## <a name="windows-hardware-dev-center-dashboard"></a>Windows ハードウェア デベロッパー センター ダッシュボード

Windows 10 Version 1809 では、開発者、IHV、OEM 用の[ハードウェア API](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-api) でドライバー パッケージを追跡して Windows ハードウェア ダッシュボードに送信できるように、新機能の追加と機能強化が行われました。

出荷ラベル REST API (ドライバーを配布するためのメソッド) を使って、出荷ラベルの作成と管理を行います。

* [Manage Shipping Labels (出荷ラベルを管理する)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/manage-shipping-labels)
* [Get shipping label data (出荷ラベルのデータを取得する)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-shipping-labels)

ドライバーのエラーや OEM ハードウェアのエラーに関するレポート データにアクセスするには、非同期のカスタム レポート メソッドを使います。 ニーズに基づいてレポート テンプレートを定義し、スケジュール設定すれば、データが定期的に届くようになります。

* [Schedule custom reports for your driver failure details (ドライバー エラー詳細のカスタム レポートをスケジュールする)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/schedule-custom-reports-for-driver-failure-details)

## <a name="debugging"></a>デバッグ

Windows 10 バージョン1809のデバッガーには、次のような変更が加えられています。

* **新しいデバッガー データ モデル API** – デバッガーの自動化をサポートするオブジェクト指向の新しいデバッガー データ モデル インターフェイスが、dbgmodel.h ヘッダーを通じて利用可能になりました。 このデバッガー データ モデルは、新しいデバッガー拡張機能 (JavaScript、NatVis、C++ で記述されたものを含む) でデバッガーからの情報を利用したり、デバッガーや他の拡張機能からアクセスできる情報を生成したりするしくみの中心となる、拡張可能なオブジェクト モデルです。 データ モデル API に書き込まれるコンストラクトは、デバッガーの dx 式エバリュエーターのほか、JavaScript 拡張機能や C++ 拡張機能から参照できます。 ドキュメントは、「[Overview of the Debugger Data Model C++ Interface (デバッガー データ モデル C++ インターフェイスの概要)](debugger/data-model-cpp-overview.md)」および [dbgmodel.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/) ヘッダーのリファレンス トピックでご覧いただけます。

* **IPv6** - Microsoft では、KDNET に IPv6 のサポートを追加しています。 IPv6 で必要とされる大きいサイズのヘッダーに対応するため、パケットのペイロード サイズを縮小しました。 その結果、KDNET プロトコルの新しいバージョンを発表して、最新バージョンのデバッガーを実行するホスト PC から IPv4 のみをサポートするターゲット PC をデバッグできるようにしています。 IPv6 をサポートするバージョンの WinDbg プレビューは、[https://aka.ms/windbgpreview](https://aka.ms/windbgpreview) でダウンロードできます。 KDNET での IPv6 のサポートに関する最新情報を入手するには、Debugging Tools for Windows ブログをフォローしてください。また、「[Setting Up KDNET Network Kernel Debugging Manually (KDNET ネットワーク カーネルのデバッグを手作業でセットアップする)](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)」で詳細をご確認ください。

## <a name="device-and-driver-installation"></a>デバイスとドライバーのインストール

Windows 10 Version 1809 では、次のコンテンツが追加されました。

* [INF AddEventProvider ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addeventprovider-directive)
* [INF DDInstall.Events セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-events-section)

次のものが更新されました。

* [起動時マルウェア対策の要件](https://docs.microsoft.com/windows-hardware/drivers/install/elam-driver-requirements)
* [カーネル モードのコード署名の要件](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-requirements--windows-vista-and-later-)

## <a name="display"></a><a name="display-1809"></a>ディスプレイ

Windows 10 Version 1809 では、ディスプレイ ドライバー開発に関する次の更新が行われました。

* **レイトレーシング** ハードウェア アクセラレータによるレイトレーシングをサポートするために、Direct3D API と平行して新しい Direct3D DDI が作成されました。 次のような DDI があります。[PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054)、[PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)。 レイトレーシングについて詳しくは、[Microsoft DirectX レイトレーシングに関する発表](https://devblogs.microsoft.com/directx/announcing-microsoft-directx-raytracing/)をご覧ください。

* **ユニバーサル ドライバーの要件** WDDM 2.5 ドライバーでは、DirectX11 UMD、DirectX12 UMD、KMD、およびこれらのコンポーネントによって読み込まれるその他すべての DLL を、ユニバーサル API に確実に準拠させる必要があります。

* **SRV のみタイル リソース階層 3** Windows 10 Version 1809 では、GPU によって、タイル リソース階層 3 の機能が直交ではない方法でサポートされます。 Direct3D12 では、順序指定されていないアクセスやレンダー ターゲットの操作を必要とせずに、スパース ボリューム テクスチャがサポートされるようになりました。 SRV のみのタイル リソース階層 3 は、階層 2 と階層 3 の間に収まる概念上の階層です。 直交タイル リソース階層 3 のサポートが現在省略可能であるのと同様に、ハードウェアのサポートは省略可能です。 ただし、SRV のみのタイル リソース階層 3 はスーパーセットの階層なので、これをサポートするにはタイル リソース階層 2 のサポートが必要です。

   直交タイル リソース階層 3 のサポートが既にドライバーでアドバタイズされている場合、最新の "オプション キャプ" の DDI 構造バージョンをサポートするためにドライバーを更新する必要はありません。 直交タイル リソース階層 3 を既にサポートしているすべてのハードウェアについて、ランタイムで SRV のみのタイル リソース階層 3 のサポートがアプリケーションにアドバタイズされます。

* **レンダリング パス** レンダリング パス機能が追加され、次のことが可能になりました。

  * 新しい API が既存のドライバーで実行できるようにする。
  * ユーザー モードのドライバーが大量の CPU を消費することなく、最適なレンダリング パスを選択できるようにする。

* **メタコマンド** メタコマンドは、IHV 高速化アルゴリズムを表す Direct3D12 オブジェクトです。 ドライバーによって実装されるコマンド ジェネレーターを非透過的に参照します。 メタコマンドの更新には、記述子テーブルのバインドやテクスチャのバインドなどが含まれます。 「[D3D12DDI_META_COMMAND_PARAMETER_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_meta_command_parameter_type)」および「[D3D12DDIARG_META_COMMAND_PARAMETER_DESC](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_meta_command_parameter_desc)」を参照してください。

  計算アルゴリズムでのテクスチャ リソース (スウィズル メモリ) の使用を有効にする
  * グラフィックス パイプライン アルゴリズムを有効にする

* **HDR 明るさ補正** SDR コンテンツの基準白色をユーザーの望む値にするために、新しい SDR 明るさブーストが導入されました。これにより、ユーザーが SDR ディスプレイに期待する明るさと同等の、標準的な 200 から 240 ニットで SDR コンテンツが再現されます。 SDR 明るさブーストは、次の 2 点において Brightness3 の動作全般に影響します。

  1. このブーストは、SDR コンテンツの事前ブレンドだけに適用されます。 HDR コンテンツへの影響はありません。 一方、ほとんどのラップトップ/brightness3 のシナリオで、ユーザーはすべてのコンテンツ (SDR と HDR) が調整されることを期待します。
  2. OS の Brightness3 スタックで望ましいニット値が判断されるとき、既に適用されている SDR ブーストは認識されません。

     そこで、HDR 用の Brightness3 DDI からのニット値が望ましい値になるように、ドライバーが補正を適用する必要があります。 グラフィックス ドライバー (およびダウンストリームの TCON など) は、望ましいニット値を得るためにコンテンツのピクセル値を変更します。そのため、アプリケーション ([D3DDDI_HDR_METADATA_HDR10](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_hdr_metadata_hdr10) を通じて) または OS の既定値 ([DxgkDdiSetTargetAdjustedColorimetry](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry) を通じて) によって提供されたとおりに HDR コンテンツ メタデータに適用される補正もあります。 グラフィックス ドライバー (TCON) がピクセル データの変更を行うため、HDR コンテンツ メタデータの補正もドライバーが行います。

* **HDR ピクセル形式のサポート** このカーネル モードのデバイス ドライバー インターフェイス (DDI) の変更は、ドライバー/デバイスによって報告される新機能を公開する WDDM 2.5 の一部で、ドライバー/デバイスによってサポートされる HDR 機能に関する情報を提供します。

   現在、ドライバー/デバイスで HDR がサポートされているかどうかは、[DdiUpdateMonitorLinkInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo) から読み取られる [DXGK_MONITORLINKINFO_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities) 構造体の *HighColorSpace* ビットに基づいて、OS で判断されます。 *HighColorSpace* ビットでは、HDR モードで実行するためのドライバー/リンク/モニター機能の組み合わせが提供されます。

    ドライバーによって報告される HDR 機能にドライバー/デバイス レベルの機能が含まれるようになりました。これにより、ドライバー/デバイスで True HDR (FP16HDR) がサポートされているか、または制限付き HDR (ARGB10HDR) のみがサポートされているかを OS で判断することができます (下の定義を参照)。

  * FP16HDR:ドライバー/デバイスは、スキャンアウト パイプラインで出力信号が HDR10 に変換されている間に、scRGB/CCC 色空間と共に FP16 ピクセル形式のサーフェスを取得して、PQ/2084 エンコードと BT.2020 プライマリを適用することができます。
  * ARGB10HDR:ドライバー/デバイスは、既に PQ/2084 でエンコードされている ARGB10 ピクセル形式のサーフェスを取得して、HDR10 信号をスキャン アウトすることができます。 ドライバー/デバイスでは、上の定義どおり FP16HDR を処理できないか、または scRGB FP16 の拡張された数値範囲を処理できません。

    グラフィックス ドライバーは、FP16HDR か ARGB10HDR のいずれかをサポート対象として報告できます。グラフィックス ドライバーはスーパーセット/サブセットの構成ではなく、FP16HDR と ARGB10HDR の両方が同時にサポート対象として報告されると、OS によるアダプターの起動が失敗するためです。 「[DXGK_MONITORLINKINFO_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities)」および「[_DXGK_DISPLAY_DRIVERCAPS_EXTENSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_display_drivercaps_extension)」を参照してください。

* **SDR ホワイト レベル** カーネル モードのデバイス ドライバー インターフェイスに既存の DDI への新しいパラメーターが追加されました。これにより、グラフィックス ドライバーは、HDR モードで実行しているディスプレイについて、OS のコンポジターがすべての SDR コンテンツに適用している "SDR ホワイト レベル" の値を知ることができます。 「_DXGK_COLORIMETRY」を参照してください。

## <a name="windows-kernel"></a><a name="kernel-1809"></a>Windows カーネル

コア カーネルに新しい API がいくつか追加されています。

* [RtlQueryRegistryValueWithFallback 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlqueryregistryvaluewithfallback):プライマリ ハンドルが存在しないときにフォールバック ハンドルを使ってレジストリ値のエントリを照会します。
* [PsGetSiloContainerId 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetsilocontainerid)と [PsGetThreadServerSilo 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetthreadserversilo)
* 次の新しい情報クラスが [_FILE_INFORMATION_CLASS](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class) に追加されました。
  * FileLinkInformationExBypassAccessCheck
  * FileCaseSensitiveInformationForceAccessCheck
  * FileStorageReserveIdInformation
    * FileLinkInformationEx
* NtCreateSection の拡張バージョンが、実際には AWE セクションであることを示すために、[NtCreateSectionEx 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatesectionex)に追加されました。
* 新しい Ex マクロは、Ntoskernel によってエクスポートされる実際のプッシュ ロック API に直接アクセスを付与します。
  * [ExAcquirePushLockExclusive マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirepushlockexclusive)
  * [ExAcquirePushLockShared マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirepushlockshared)
  * [ExInitializePushLock 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepushlock)
  * [ExReleasePushLockExclusive マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleasepushlockexclusive)
  * [ExReleasePushLockShared マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleasepushlockshared)
* [KzLowerIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kzlowerirql) と [KzRaiseIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kzraiseirql) は、フォワーダに依存してインライン関数の特殊なケースをインスタンス化するのではなく、Windows 8 以降のバージョンをターゲットとするカーネル コンポーネントでサポートされる extern forceinline に移動されました。
* PCI の Flattening Portal Bridge (FPB) がサポートされるようになりました。 詳しくは、[正式な仕様](https://pcisig.com/sites/default/files/specification_documents/ECN_FPB_9_Feb_2017.pdf)をご覧ください。 新しい API (_PCI_FPB_*) が [Ntddk.h](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/) で宣言されています。

## <a name="networking"></a><a name="networking-1809"></a>ネットワーク

## <a name="netadaptercx"></a>NetAdapterCx

* [NetAdapterCx クライアント ドライバーの INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/netcx/inf-files-for-netadaptercx-client-drivers)に関する新しいトピック。
* API サーフェスを簡略化するために、キューの送受信がパケット キューと呼ばれる単一のオブジェクトの種類に統合されました。 「[Transmit and receive queues (キューの送信および受信)](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues)」トピックに「[Polling model (ポーリング モデル)](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues#polling-model)」という新しいセクションが追加されました。
* [ハードウェア オフロード](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-hardware-offloads)が NetAdapterCx に追加されており、関連するパケット拡張機能のクライアント ドライバーへの登録も自動化されます。
* ネットワーク インターフェイスがドライバーの WDF デバイス オブジェクトから切り離されました。 これをサポートするために、*EvtNetAdapterSetCapabilities* コールバック関数が削除されました。 NetAdapterCx クライアント ドライバーは、既定のものを含め複数のネットワーク インターフェイスを持てるようになりました。

   ネットワーク インターフェイスとデバイス オブジェクトの分離をサポートするために、次のトピックが更新されました。

  * [Summary of NetAdapterCx objects (NetAdapterCx オブジェクトの概要)](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-netadaptercx-objects)
  * [Device and adapter initialization (デバイスとアダプターの初期化)](https://docs.microsoft.com/windows-hardware/drivers/netcx/device-and-adapter-initialization)
  * [Power-up sequence for a NetAdapterCx client driver (NetAdapterCx クライアント ドライバーの電源投入シーケンス)](https://docs.microsoft.com/windows-hardware/drivers/netcx/power-up-sequence-for-a-netadaptercx-client-driver)
  * [Power-down sequence for a NetAdapterCx client driver (NetAdapterCx クライアント ドライバーの電源切断シーケンス)](https://docs.microsoft.com/windows-hardware/drivers/netcx/power-down-sequence-for-a-netadaptercx-client-driver)

* [NetAdapterCx の Receive Side Scaling (RSS)](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-receive-side-scaling-rss-) をサポートする DDI が簡略化されました。
* パケット コンテキスト トークン ヘルパー マクロが削除されました。

## <a name="ndis"></a>NDIS

[Receive Side Scaling バージョン 2 (RSSv2)](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-) がバージョン 1.01 に更新されました。

## <a name="mobile-broadband"></a><a name="mobilebroadband-1809"></a>モバイル ブロードバンド

* MBB デバイスのマルチ パケット データ プロトコル (MPDP) インターフェイスをサポートする新しい [OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-mpdp) と DDI。
* MBB デバイスとドライバーのリセット回復の信頼性を高める新しい[デバイスベースのリセットと回復](https://docs.microsoft.com/windows-hardware/drivers/network/mb-device-based-reset-and-recovery)機能。

## <a name="mobile-broadband-wdf-class-extension-mbbcx"></a>モバイル ブロードバンド WDF クラス拡張機能 (MBBCx)

MBBCx 電源管理の方法が簡略化されました。

Windows 10 Version 1803 では MBBCx のプレビュー コンテンツが提供されていましたが、現在、MBBCx は Windows 10 Version 1809 バージョンの WDK に付属するようになりました。

## <a name="mobile-operators"></a>携帯電話会社

[AutoConnectOrder 設定](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings#apn-database-and-desktop-cosa-settings)がデスクトップ COSA でサポートされるようになりました。

## <a name="sensors"></a><a name="sensors-1809"></a>センサー

明るさの自動調整機能のサポート:

センサーでの明るさの自動調整をサポートするために、PKEY_SensorData_IsValid データ フィールドが追加されました。

詳しくは、「[Light sensor data fields (光センサー データ フィールド)](https://docs.microsoft.com/windows-hardware/drivers/sensors/light-sensor-data-fields)」をご覧ください。

## <a name="universal-drivers-in-windows-10-version-1809"></a>Windows 10 Version 1809 のユニバーサル ドライバー

Windows 10 Version 1809 以降、Windows で柔軟なリンクがサポートされるようになりました。これにより、単一のバイナリを使って OneCore およびデスクトップの SKU をターゲットとすることができます。
柔軟なリンクを有効にするには、次の新しい SDK API を使用します。

* [IsApiSetImplemented](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented)

この既存のトピックが補強され、柔軟なリンクを使って [DCHU ドライバー設計の原則](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers#design-principles)に関する U の要件に準拠する方法についての説明が加わりました。

* [OneCore をターゲットとしたビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-for-onecore)


## <a name="usb"></a><a name="usb-1809"></a>USB

**USB Type-C ドライバー開発者向けの新機能:**

お使いのハードウェアが UCSI に準拠しており、非 ACPI トランスポート経由の通信が必要な場合は、新しいクラス拡張機能 &mdash; (UcmUcsiCx.sys) を利用できます。 これは、トランスポートに依存しない方法で UCSI 仕様を実装します。 最小限のコードで、UcmUcsiCx へのクライアントであるドライバーが非 ACPI トランスポート経由で USB Type-C ハードウェアと通信できます。 このトピックでは、UCSI クラス拡張機能で提供されるサービスと、クライアント ドライバーの想定される動作について説明します。

* [Write a UCSI client driver (UCSI クライアント ドライバーの作成)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-ucsi-driver)
* [UcmUcsiCx クラス拡張機能のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)
* [UcmUcsiCx クライアント ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

**USB Type-C ドライバー開発者向けの新機能により、USB Type-C コネクタのアクティビティを監視したり、USB Type-C コネクタに関するポリシーの決定に関与したりすることが可能になりました。**

たとえば、温熱条件に基づいてデバイスの充電を制御して、デバイスの過熱を防ぐことができます。

* [Write a USB Type-C Policy Manager client driver (USB Type-C ポリシー マネージャー クライアント ドライバーの作成)](https://www.microsoft.com/windows-hardware/drivers/usbcon/policy-manager-client)
* [Usbpmapi.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/) で利用可能な新しい API

**エミュレートされた USB デバイス (UDE) で利用可能なクラス拡張機能の新しいバージョン-- 1.1 および USB ホスト コントローラー (Ucx) 1.5:**

エミュレートされたデバイスで、機能のリセット (FLDR) やプラットフォームのリセット (PLDR) による、より信頼性の高いリセット回復がサポートされるようになりました。 クライアント ドライバーからシステムに、デバイスのリセットが必要であることと、リセットの種類 (機能またはプラットフォーム) を通知できるようになりました。

* [UdecxWdfDeviceNeedsReset 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

ホスト コントローラーでも、以下を通じて FLDR と PLDR のリセットを行えます。

* [EVT_UCX_USBDEVICE_DISABLE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)

## <a name="wi-fi"></a><a name="wifi-1809"></a>Wi-Fi

WLAN デバイス ドライバー インターフェイス (WDI) 仕様がバージョン 1.1.7 に更新されました。

* WDI ドライバーの最新の 802.11ax PHY タイプのサポートが追加されました。
* 承諾されていないデバイス サービスの状態表示のサポートが追加されました。