---
title: Windows 10 バージョン1803のドライバー開発の変更点
description: このセクションでは、Windows 10 でのドライバー開発に関する新機能について説明します。
ms.assetid: 73ba8c40-d605-4dba-a965-0a87d80b9126
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4b86d647cc1ae42e8a6221860fe63869b61a044a
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270421"
---
# <a name="whats-new-in-windows-10-version-1803"></a>Windows 10 バージョン 1803 の新機能

このセクションでは、Windows 10 Version 1803 (Windows 10 April 2018 Update) でのドライバー開発に関する新機能と更新された機能について説明します。

## <a name="acpi"></a><a name="acpi-1803"></a>ACPI

Windows 10 Version 1803 では、プラットフォームの機能と物理デバイスの位置情報をサポートするために、ACPI の DDI が更新されています。

## <a name="audio"></a><a name="audio-1803"></a>オーディオ

[音声による有効化](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)に関するトピックが更新され、APO 要件に関する情報が追加されました。

## <a name="bluetooth"></a><a name="bluetooth-1803"></a>Bluetooth

Windows 10 Version 1803 では、クイック ペアリングのサポートが導入されます。 ユーザーが設定アプリに移動して、ペア設定する周辺機器を検索する必要がなくなりました。 使用可能な新しい周辺機器が近くで検出されると、Windows によって通知がポップアップ表示されます。 お使いの周辺機器をクイック ペアリングに確実に対応させるには、2 つの要件セットがあります。 1 つは周辺機器の動作に関するもので、もう 1 つは Microsoft が定義したベンダーのアドバタイズ セクションの構造と値に関するものです。 詳細については、次のドキュメントを参照してください。

* [Bluetooth クイック ペアリング](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth-swift-pair)
* [Bluetooth の機能と推奨事項](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)

Windows 10 Version 1803 では Bluetooth バージョン 5.0 がサポートされます。 プロファイルのサポートについては、「[Bluetooth Version and Profile Support in Windows 10 (Windows 10 での Bluetooth バージョンとプロファイルのサポート)](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/general-bluetooth-support-in-windows)」をご覧ください。

## <a name="camera"></a><a name="camera-1803"></a>カメラ

カメラ ドライバーの開発では、次の更新が行われました。

* [DShow Bridge implementation guidance for UVC devices (UVC デバイス向け DShow (DirectShow) ブリッジ実装ガイド)](https://docs.microsoft.com/windows-hardware/drivers/stream/dshow-bridge-implementation-guidance-for-usb-video-class-devices) - USB ビデオ クラス (UVC) 仕様に準拠しているカメラとデバイス向けに DShow ブリッジを構成するための実装ガイド。 このプラットフォームは、USB バス標準から Microsoft OS 記述子を使って DShow ブリッジを構成します。 拡張プロパティ OS 記述子は USB の標準的な記述子の拡張機能です。標準仕様では有効にされない Windows 固有のデバイス プロパティを返すために、USB デバイスによって使用されます。
* [360 カメラのビデオ キャプチャ](https://docs.microsoft.com/windows-hardware/drivers/stream/360-camera-video-capture) - 既存の MediaCapture API を使い、360 カメラのプレビュー、キャプチャ、録画のサポートを提供します。 これにより、プラットフォームで球面のフレーム ソース (正距円筒図法のフレームなど) を公開することができ、アプリで 360 カメラのビデオ ストリームを検出して処理するだけでなく、360 キャプチャ エクスペリエンスを提供することが可能になります。

## <a name="debugging"></a>デバッグ

Windows 10 バージョン1803のデバッガーには、次のような変更が加えられています。

[WinDbg プレビューのタイム トラベル デバッグ (TTD) ハンズオン ラボ](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-walkthrough) - このラボでは、コードにエラーのある短いサンプル プログラムを使ってタイム トラベル デバッグ (TTD) を紹介します。 TTD を使って問題をデバッグし、その根本原因を特定します。

## <a name="display"></a><a name="display-1803"></a>ディスプレイ

Windows 10 Version 1803 では、ディスプレイ ドライバー開発に関する次の更新が行われました。

* **間接ディスプレイ UMDF クラス拡張機能** - 間接ディスプレイ ドライバーは、レンダリング GPU に SRM を渡すことができ、使用中の SRM バージョンを問い合わせるメカニズムを持つことができます。

* **IOMMU ハードウェア ベースの GPU 分離のサポート** - システム メモリへの GPU アクセスを制限することで、セキュリティを向上させます。

* **GPU 準仮想化のサポート** - ディスプレイ ドライバーが Hyper-V 仮想化環境にレンダリング機能を提供できるようにします。

* **明るさ** - マルチ ディスプレイをサポートする新しい明るさインターフェイスで、調整されたニット ベースの明るさレベルに設定することができます。

* **D3D11 ビットストリーム暗号化** - 8 バイトまたは 16 バイトの初期化ベクトルを使用する CENC、CENS、CBC1、および CBCS の公開をサポートするために D3D11 に追加された GUID とパラメーター。

* **D3D11 と D3D12 のビデオ デコード ヒストグラム** - 輝度ヒストグラムにより、メディア チームがヒストグラムの固定機能ハードウェアを活用して、HDR/EDR のシナリオにおけるトーン マッピングの品質を向上させることができます。 固定機能ハードウェアは、これらのシナリオで GPU が既に飽和状態にあり、並列処理を有効にする場合に便利です。 この機能は省略可能です。固定機能ハードウェアが利用できる場合にのみ実装してください。 この機能は 3D または計算を使って実装しないでください。

* **D3D12 ビデオ デコード**でデコード階層 II がサポートされるようになりました。これは、ドライバーで "*テクスチャの配列*" がサポートされることにより、アプリケーションが割り当てコストを償却し、解像度の変更中にピーク時のメモリ使用量を削減できることを意味します。

* **タイル リソース階層と LDA アトミック** - リンクされたアダプター (LDA) ノード間で機能するアトミック シェーダー命令のサポートを追加する新しいクロス ノード共有階層。 これにより、ISV が分割フレーム レンダリング (SFR) などの GPU レンダリング手法を複数実装することができるため、D3D11 で実現可能な機能が明らかに向上します。

* **GPU ディザリングのサポート** - ドライバーは、特定の時点のモードに対して有線信号でディザリングを実行できるかどうかを報告できます。 これにより、モニター リンクで物理的に使用可能なものよりも高い有効ビット深度が必要なシナリオ (HDMI 2.0 を介した HDR10 など) で、OS が明示的にディザリングを要求できます。

* **後処理による色調整のオーバーライド**- ディスプレイの色を調整または変更するようなすべての後処理を一時的に無効にするよう、OS からドライバーに要求できるようにします。 これは、特定のアプリケーションがディスプレイでの比色分析による正確な色動作を強制するシナリオをサポートし、OEM または IHV 独自のディスプレイの色調整と安全に共存します。

* **Direct3D12 とビデオ** - 次の機能へのアクセスを提供する新しい API と DDI:
  * ハードウェア アクセラレータによるビデオのデコード
  * コンテンツの保護
  * ビデオの処理

* **DisplayID** - グラフィックス アダプターによって制御されているディスプレイから VESA の DisplayID 記述子を問い合わせることができるように設計され、DisplayID v1.3 と DisplayID v2.0 をサポートする新しい DDI。 この DDI は既存の DxgkDdiQueryAdapterInfo DDI の拡張機能であり、カーネル モードのディスプレイ専用ドライバーや間接ディスプレイ ドライバーを含む、DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM2_3 のすべてのドライバーでサポートされます。

* **GPU パフォーマンス データ** - DdiQueryAdapterInfo の拡張機能により、温度、ファン速度、エンジンおよびメモリのクロック速度、メモリ帯域幅、電力、電圧などの情報が公開されます。

* その他 - IHV による新しいドライバーのオンボードに役立つ新しい SupportContextlessPresent ドライバー キャップ。

* OS での外部/リムーバブル GPU サポートの強化。 優れたサポートを追加する最初の手順として、Dxgkrnl では GPU が "切り離し可能" (ホットプラグ可能) かどうかを判断する必要があります。 RS4 では、独自のインフラストラクチャを構築する代わりに、ドライバーのこの情報を活用します。 このため、DXGK_ DRIVERCAPS 構造体に "Detachable" ビットが追加されています。 アダプターがホットプラグ可能な場合、アダプターの初期化中にドライバーによってこのビットが設定されます。

* **ディスプレイ診断** - カーネル モードのデバイス ドライバー インターフェイス (DDI) が変更され、ディスプレイ コントローラーのドライバーから OS に診断イベントを報告できるようになりました。  ドライバーはこのチャネルを通じて、(OS の要求に対する応答でも、OS による対応が必要なものでもないため) 通常は OS で認識されないイベントのログを記録することができます。

* **共有グラフィックス電源コンポーネント** - 非グラフィックス ドライバーでグラフィックス デバイスの電源管理を行えるようにします。  非グラフィックス ドライバーはグラフィックス ドライバーと連携し、ドライバー インターフェイスを介して 1 つ以上の共有電源コンポーネントを管理します。

* **共有テクスチャの機能強化** - プロセスや D3D デバイス間で共有可能なテクスチャの種類が増えました。 この設計により、最小限のメモリのコピーだけで、フレーム サーバーの OS コンポーネントでモノクロがサポートされるようになります。

## <a name="driver-security"></a><a name="security-1803"></a>ドライバーのセキュリティ

[Windows ドライバー セキュリティ ガイダンス](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/)と、ドライバー開発者向けにドライバー セキュリティのチェックリストを提供する[ドライバー セキュリティ チェックリスト](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/driver-security-checklist)が更新されました。

## <a name="windows-kernel"></a><a name="kernel-1803"></a>Windows カーネル

このセクションでは、Windows 10 Version 1803 での Windows カーネル ドライバー開発に関する新機能と更新された機能について説明します。

サード パーティが独自の KDNET 拡張性モジュールや KdSerial トランスポート レイヤーを作成できるように、新しい API のセットがキットに追加されました。 サンプル コードについては、Debuggers フォルダーの "カーネル トランスポート サンプル" (ddk\samples\kdserial および ddk\samples\kdnet) をご覧ください。

ファイルの状態を格納する場所として、(オペレーティング システムで認識されている) 承認された場所をドライバーに提供するためのサポートが追加されました。  この方法により、システムが格納場所にあるファイルをデバイスやドライバーと関連付けることができます。

ファイルの状態が格納される場所は、ドライバーの内部構成ごと、およびデバイスごとにそれぞれ異なります。 ファイルの状態を持つドライバーに対して、次のどちらの状態をディスクに書き込むかを指定できます。

* ドライバーの状態 ([IoGetDriverDirectory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdriverdirectory)): 複数のデバイスを制御している可能性があるドライバーに対してグローバル、または

* デバイスの状態 ([IoGetDeviceDirectory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicedirectory)): ドライバーによって制御される単一のデバイスに固有の値で、他のデバイスでは同様の状態であっても値が異なる場合があります。

機能ドライバー (FDO) で、それぞれの PCIe デバイスが D3Cold 状態にあるとき、追加の電力をネゴシエートできるようになりました。 たとえば、次のようなアニメーションや効果を作成できます。

* 補助電源要件 [D3COLD_REQUEST_AUX_POWER](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-d3cold_request_aux_power)。
* コア電源レール [D3COLD_REQUEST_CORE_POWER_RAIL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-d3cold_request_core_power_rail)。
* システムが ACPI 動作状態にあり、対応するエンドポイントまたは PCI Express アップストリーム ポートが D3cold に遷移する間に、PCI Express ダウンストリーム ポートでメッセージを受信してからプラットフォームがスロットに PERST# をアサートするまでの固定遅延時間の要件。 「[D3COLD_REQUEST_PERST_DELAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-d3cold_request_perst_delay)」を参照してください。

NT サービスおよびカーネル モードとユーザー モードのドライバーは、[RtlRaiseCustomSystemEventTrigger](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlraisecustomsystemeventtrigger) 関数を使うことで、デバイスに対してカスタム トリガーを実行することができます。 ドライバーの開発者が所有するカスタム トリガーは、カスタム トリガー ID によって識別される関連バック グラウンド タスクを開始するよう、システムのイベント ブローカーに通知します。

アクティブ セッションの変更通知に登録して、通知が発生したときにコールバックを取得できるようになりました。 この通知の一環として、一部のデータが呼び出し元で共有されます。 この関連付けられているデータは、[PO_SPR_ACTIVE_SESSION_DATA 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntpoapi/ns-ntpoapi-_po_spr_active_session_data)を介して配信されます。

## <a name="networking"></a><a name="networking-1803"></a>ネットワーク

このセクションでは、Windows 10 Version 1803 での Windows ネットワーク ドライバー開発に関する新機能と強化された機能について簡単に説明します。

## <a name="ndis-and-netadaptercx"></a>NDIS および NetAdapterCx

NDIS では次の更新が行われました。

* [Receive Side Scaling V2](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-in-ndis-6-80) が更新され、ステアリング パラメーターに関する詳細情報が追加されました。
* [同期 OID インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/synchronous-oid-request-interface-in-ndis-6-80)で NDIS 軽量フィルター ドライバーがサポートされるようになりました。

ネットワーク アダプターの WDF クラス拡張機能 (NetAdapterCx) に関する次のトピックが新たに追加されました。

* [NetAdapterCx 1.2 の概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/introduction-to-netadaptercx-1-2)
* [Packet descriptors and extensions (パケットの記述子と拡張機能)](https://docs.microsoft.com/windows-hardware/drivers/netcx/packet-descriptors-and-extensions)
* [Network data buffer management (ネットワーク データ バッファーの管理)](https://docs.microsoft.com/windows-hardware/drivers/netcx/network-data-buffer-management)
* [NetAdapterCx Receive Side Scaling (RSS)](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-receive-side-scaling-rss-)

さらに、モバイル ブロードバンド クラス拡張機能 (MBBCx) に関する新しいトピックも追加されました。これは、モバイル ブロードバンド接続に NetAdapterCx モデルを使用するプレビュー専用の機能です。

* [Mobile Broadband Class Extension (MBBCx) (モバイル ブロードバンド クラス拡張機能 (MBBCx))](https://docs.microsoft.com/windows-hardware/drivers/netcx/mobile-broadband-mbb-wdf-class-extension-mbbcx-)
  * [Writing an MBBCx client driver (MBBCx クライアント ドライバーの作成)](https://docs.microsoft.com/windows-hardware/drivers/netcx/writing-an-mbbcx-client-driver)
  * [MBBCx API リファレンス](https://docs.microsoft.com/windows-hardware/drivers/netcx/mbbcx-api-reference)

## <a name="mobile-broadband"></a><a name="mobilebroadband-1803"></a>モバイル ブロードバンド

モバイル ブロードバンドについては、[MB 低レベル UICC アクセス](https://docs.microsoft.com/windows-hardware/drivers/network/mb-low-level-uicc-access)について詳しく説明した新しいトピックが追加されました。

## <a name="mobile-operators"></a>携帯電話会社

新しいホットスポットと AppID の設定が[デスクトップ COSA](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings#desktop-cosa-only-settings) の一部になりました。 通信事業者が [Sysdev メタデータ パッケージ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata)を使ってブロードバンド アプリ エクスペリエンスのアプリを提供している場合は、[MO UWP アプリ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/uwp-mobile-broadband-apps)と [COSA データベース](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings)に移行することを強くお勧めします。

## <a name="pcie"></a><a name="pci-1803"></a>PCIe

次のモダン スタンバイと PCI ホット プラグのシナリオをサポートするために、新しい ACPI _DSD メソッドが追加されました。

* PCIe ルート ポートでの DDRIPS (指示された最も深いランタイム アイドル電源状態) のサポート
* D3 でのホット プラグをサポートする PCIe ルート ポートの識別
* 外部に公開されている PCIe ルート ポートの識別

詳しくは、「[ACPI Interface:Device Specific Data (_DSD) for PCIe Root Ports (ACPI インターフェイス: PCIe ルート ポートのデバイス固有のデータ (_DSD))](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports)」をご覧ください。

## <a name="sensors"></a><a name="sensors-1803"></a>センサー

接続の種類のプロパティを明確にするために、[SENSOR_CONNECTION_TYPES 列挙](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-sensor_connection_types)が追加されました。

## <a name="usb"></a><a name="usb-1803"></a>USB

共有コネクタのデタッチをシミュレートするための新しい API が追加されました。 USB デバイスがホストに接続されているか共有コネクタを持っている場合、スタックが削除されるときにデバイスがホストに接続されているか共有コネクタを持っていれば、デタッチ イベントをシミュレートできます。 この時点ですべてのアタッチ/デタッチ通知メカニズムが無効になります。 詳しくは、「[UfxDeviceNotifyFinalExit 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyfinalexit)」をご覧ください。

## <a name="wi-fi"></a><a name="wifi-1803"></a>Wi-Fi

Wi-Fi ドライバーの開発では、[高度な電源管理機能である Nic Auto Power Saver (NAPS) の TLV](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-os-power-management-features) が新たに追加され、プラットフォーム レベルのデバイス回復サービス (PLDR) が更新されています。
