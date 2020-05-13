---
title: Windows 10 バージョン1709のドライバー開発の変更点
description: このセクションでは、Windows 10 でのドライバー開発に関する新機能について説明します。
ms.assetid: 68a5a513-0dab-40f7-b67f-29b76061e1ab
ms.date: 04/14/2020
author: EliotSeattle
ms.localizationpriority: medium
ms.openlocfilehash: f444681a72873e357cc61109672a28145ea0ffee
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270423"
---
# <a name="driver-development-additions-for-windows-10-version-1709"></a>Windows 10 バージョン1709のドライバー開発の追加

このトピックでは、Windows 10 バージョン1709での Windows ドライバー開発に関する機能と更新プログラムについて説明します。

## <a name="feature-areas-updated-in-windows-10-version-1709"></a>Windows 10 バージョン1709で更新された機能領域

次の機能には、Windows 10 バージョン1709の更新プログラムが記載されています。

- [オーディオ](#audio)
- [ACPI](#acpi)
- [生体認証](#biometric)
- [Windows デバッガー](#windows-debugger)
- [表示](#display)
- [ドライバーの検証](#driver-verifier)
- [ハードウェア通知](#hardware-notifications)
- [Windows カーネル](#windows-kernel)
- [モバイル ブロードバンド](#mobile-broadband)
- [ネットワーク](#networking)
- [仮想 PCI](#virtualized-pci)
- [パルス幅変調](#pulse-width-modulation-controllers)
- [ファイルシステム & ストレージ](#file-systems-and-storage)
- [USB](#usb)
- [ユニバーサル Windows ドライバー](#universal-windows-drivers)
- [WPP ソフトウェア トレース](#wpp-software-tracing)

### <a name="windows-debugger"></a>Windows デバッガー

Windows 10 Version 1709 では、デバッガーに関する次のコンテンツ セットが新たに追加されています。

- [Debugging Using WinDbg Preview (WinDbg プレビューを使用したデバッグ)](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-using-windbg-preview) - 次世代のデバッガーをプレビューします。
- [Time Travel Debugging - Overview (タイム トラベル デバッグ - 概要)](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-overview) - プロセスの実行を記録して再生します。

### <a name="driver-verifier"></a>ドライバーの検証ツール

ドライバーの検証ツールには、次のテクノロジ向けの新しいドライバー検証規則が含まれています。

- 新しい[オーディオ ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-audio-drivers)
- 新しい [AVStream ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-avstream-drivers)
- 4 つの新しい [KMDF ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/sdv-rules-for-kmdf-drivers)
- 3 つの新しい [NDIS ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/sdv-rules-for-ndis-drivers)
- 新しい [Nullcheck 規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/nullcheck) (*Version 1703 で追加*)

### <a name="universal-windows-drivers"></a>ユニバーサル Windows ドライバー

Windows 10 Version 1709 では、ユニバーサル ドライバーに次の新機能が追加されました。

- [Windows Update を使ったデバイス ファームウェアの更新](https://docs.microsoft.com/windows-hardware/drivers/install/updating-device-firmware-using-windows-update) - Windows Update (WU) サービスを使って、リムーバブルまたはシャーシ内のデバイスのファームウェアを更新する方法について説明しています。
- [Reg2inf](https://docs.microsoft.com/windows-hardware/drivers/devtest/reg2inf) - ドライバー パッケージ INF レジストリ変換ツール (reg2inf.exe) は、レジストリ キーとその値または DLL RegisterServer ルーチンを実装する COM .dll を、INF AddReg ディレクティブのセットに変換します。 これらのディレクティブは、ドライバー パッケージ INF ファイルに含まれます。

Windows 10 Version 1709 では、ユニバーサル ドライバーに関する次の更新が行われました。

- [ユニバーサル ドライバー シナリオ](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios)への新しい COM コンポーネント サンプルの追加
- [INF AddComponent ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addcomponent-directive)
- [拡張 INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)
- [コンポーネント INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)

### <a name="wpp-software-tracing"></a>WPP ソフトウェア トレース

[WPP ソフトウェアのトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)には、Windows 10 バージョン1709での*Inflight トレースレコーダー*の新機能が導入されています。 ドライバーで WPP トレースと WPP レコーダーを有効にすると、トレース ログが自動的にオンになるため、トレース セッションを開始または停止せずに簡単にメッセージを表示できます。 ログをよりきめ細かく制御できるように、WPP レコーダーでは KMDF ドライバーによるカスタム バッファーの作成と管理が許可されています。

- [ログ トレース用の WPP レコーダー](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)
- [WppRecorderLogGetDefault](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-imp_wpprecorderloggetdefault)
- [WppRecorderLogCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate) (KMDF のみ)
- [WppRecorderDumpLiveDriverData](https://docs.microsoft.com/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderdumplivedriverdata)

### <a name="audio"></a>オーディオ

Windows 10 Version 1709 では、Windows オーディオ ドライバーの開発に関する次の更新が行われました。

- 「[Configure and query audio device modules (オーディオ デバイス モジュールの構成とクエリ)](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)」が新たに追加されました。
- 「[voice activation (音声によるアクティブ化)](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)」が全面的に更新されました。
  - チェーンとキーワードのみのアクティブ化に関する詳細情報
  - 新しい用語集
  - トレーニングや認識に関する追加情報 (暗証番号やオーディオ形式の情報など)
  - 更新されたキーワード システムの概要
  - 音声によるスリープ解除に関する最新情報

### <a name="acpi"></a>ACPI

次に示すのは、Windows 10 バージョン1709の入出力バッファーをサポートする新しい高度な構成と電源インターフェイス (ACPI) DDIs の一覧です。

- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)
- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)
- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2)
- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2_ex)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2_ex)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2_ex)
- [ACPI_EVAL_INPUT_BUFFER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)
- [ACPI_EVAL_INPUT_BUFFER_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)
- [ACPI_EVAL_INPUT_BUFFER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2)
- [ACPI_EVAL_INPUT_BUFFER_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2_ex)
- [ACPI_EVAL_OUTPUT_BUFFER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)
- [ACPI_EVAL_OUTPUT_BUFFER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v2)
- [ACPI_METHOD_ARGUMENT_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)
- [ACPI_METHOD_ARGUMENT_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v2)
- [GIC_ITS](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpitabl/ns-acpitabl-_gic_its)

### <a name="biometric"></a>生体認証

Windows 10 バージョン1709で導入された Windows 生体認証ドライバーには、新しい署名要件がありました。 詳しくは、「[Signing WBDI Drivers (WBDI ドライバーへの署名)](https://docs.microsoft.com/windows-hardware/drivers/biometric/signing-wbdi-drivers)」をご覧ください。

### <a name="display"></a>ディスプレイ

Windows 10 バージョン1709での Windows Display driver の開発には、次の新機能が導入されました。

- Display ColorSpace Transform DDI により、ポストコンポジション ディスプレイ パイプラインに適用される色空間の変換をより詳細に制御できます。
- D3D12 のコピー キュー タイムスタンプ クエリ機能により、アプリケーションが COPY コマンドのリスト/キューに対してタイムスタンプ クエリを発行できるようになります。 これらのタイムスタンプを指定することで、他のエンジンのタイムスタンプと同じように機能します。
- 以下を介した Direct3D12 ランタイムへのビデオの統合が強化されました。
    1. ハードウェア アクセラレータによるビデオのデコード
    2. コンテンツの保護
    3. ビデオの処理

### <a name="hardware-notifications"></a>ハードウェア通知

Windows 10 バージョン1709では、ハードウェアに依存しない通知コンポーネント (Led や振動メカニズムなど) のサポートが追加されました。 詳細については、次のドキュメントを参照してください。

- [Hardware notifications support (ハードウェア通知のサポート)](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/hardware-notifications-support)
- [ハードウェア通知リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_gpiobtn/)

### <a name="windows-kernel"></a>Windows カーネル

Windows 10 Version 1709 では、ドライバーの Windows カーネルに新しいルーチンがいくつか追加されています。

- ExGetFirmwareType および ExIsSoftBoot &ndash; エグゼクティブ ライブラリ サポート ルーチン。
- [PsSetLoadImageNotifyRoutineEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutineex) &ndash; 実行可能なすべてのイメージ (オペレーティング システムのネイティブ アーキテクチャとは異なるアーキテクチャを持つイメージも含む) の拡張イメージ通知ルーチン。
- [MmMapMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapmdl) &ndash; メモリ記述子の一覧 (MDL) に記述されている物理ページをシステムの仮想アドレス空間にマッピングするための[メモリ マネージャー](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-memory-manager) ルーチン。
- [PoFxSetTargetDripsDevicePowerState](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsettargetdripsdevicepowerstate) &ndash; デバイスのターゲット デバイスが DRIPS の電源状態になったことを電源マネージャーに通知する PoFx ルーチン。
- プロセスポリシーに関連する[Zwsetinformationthread](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwsetinformationthread)ルーチンには、次のオプションが追加されました。

  - [PROCESS_MITIGATION_CHILD_PROCESS_POLICY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_process_mitigation_child_process_policy)
  - [PROCESS_MITIGATION_PAYLOAD_RESTRICTION_POLICY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_process_mitigation_payload_restriction_policy)
  - PROCESS_READWRITEVM_LOGGING_INFORMATION

- [PsGetServerSiloActiveConsoleId](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetserversiloactiveconsoleid) [PsGetParentSilo](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetparentsilo) &ndash; コンピューターで作成および破棄されたサーバーサイロに関する情報を取得するための PsGetServerSiloActiveConsoleId および PsGetParentSilo サイロ api。
- 以下は、イベントと生成されたログを診断目的で参照する相関関係ベクトルを使用するための新しい RTL 関数の一覧です。
  - [CORRELATION_VECTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-correlation_vector)
  - [RtlExtendCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlextendcorrelationvector)
  - [RtlIncrementCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlincrementcorrelationvector)
  - [RtlInitializeCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlinitializecorrelationvector)
  - [RtlValidateCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlvalidatecorrelationvector)

### <a name="mobile-broadband"></a>モバイル ブロードバンド

Windows 10 バージョン1709でのドライバー開発の Windows Mobile ブロードバンドおよび携帯電話のシナリオでは、次の機能が追加されました。

- [UICC のリセット](https://docs.microsoft.com/windows-hardware/drivers/network/mb-uicc-reset-operations)と[モデムのリセット](https://docs.microsoft.com/windows-hardware/drivers/network/mb-modem-reset-operations)
- [プロトコル構成操作 (PCO)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-protocol-configuration-operations--pco-)
- [基地局情報の問い合わせ](https://docs.microsoft.com/windows-hardware/drivers/network/mb-base-stations-information-query-support)
- [eSIM と MBIM ReadyState のガイダンス](https://docs.microsoft.com/windows-hardware/drivers/network/mb-esim-mbim-ready-state-guidance)

Windows 10 Version 1709 では、[デスクトップ COSA のドキュメント](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/planning-your-desktop-cosa-apn-database-submission)が更新され、ブランド関連のフィールドが新たに追加されました。
通信事業者のシナリオに関するその他の変更については、[非推奨の機能](what-s-new-in-driver-development.md#deprecated-features)の一覧をご覧ください。

### <a name="networking"></a>ネットワーク

Windows ネットワークドライバーの開発に関するこれらの新機能と機能強化は、Windows 10 バージョン1709で追加されました。

以下は、NDIS の新機能と更新された機能の一覧です。

- NewAdapterCx の新機能を含む NetAdapterCx 1.1 の概要:
  - パケット コンテキスト オプションの追加
  - リンク状態の微調整
  - 受信バッファーの管理とパフォーマンスの改善
  - 全般的なパフォーマンスの向上
- NDIS 6.80 の新しい[同期 OID 要求インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/synchronous-oid-request-interface-in-ndis-6-80)
- NDIS 6.80 の新しい [Receive Side Scaling バージョン 2 (RSSv2)](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-in-ndis-6-80)
- [NDIS 6.80 の概要](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-ndis-6-80)
- [NDIS 6.x ドライバーの NDIS 6.80 への移植](https://docs.microsoft.com/windows-hardware/drivers/network/porting-ndis-6-x-drivers-to-ndis-6-80)

### <a name="virtualized-pci"></a>仮想化 PCI

Windows 10 バージョン1709では、PCI Express シングルルート i/o 仮想化 (SR-IOV) 仕様に準拠しているデバイス用の物理関数ドライバーを作成するための新しいプログラミングインターフェイスが追加されました。 このインターフェイスは Pcivirt.h で宣言されます。 詳しくは、「[PCI virtualization (PCI の仮想化)](https://docs.microsoft.com/windows-hardware/drivers/ddi/pcivirt/)」をご覧ください。

### <a name="pulse-width-modulation-controllers"></a>パルス幅変調コントローラー

Windows 10 Version 1709 では、SoC の一部であるパルス幅変調 (PWM) コントローラーへのアクセスと SoC アドレス空間へのメモリ マップを提供するために、カーネル モードのドライバーを作成する必要があります。 詳しくは、「[PWM driver for an on-SoC PWM module (on-SoC PWM モジュールの PWM ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/spb/pulse-width-controller%20driver?branch=spb)」をご覧ください。

PIN のパスを解析して検証し、PIN 番号を抽出するには、カーネル モデル ドライバーで [PwmParsePinPath](https://docs.microsoft.com/windows-hardware/drivers/ddi/pwmutil/nf-pwmutil-pwmparsepinpath) を使用する必要があります。

アプリは [PWM IOCTL](https://docs.microsoft.com/windows-hardware/drivers/spb/pulse-width-controller%20driver#pwm-ioctl-requests) 要求を送信することで、コントローラー ドライバーに要求を送ることができます。

### <a name="file-systems-and-storage"></a>ファイルシステムとストレージ

ファイル システムとストレージでは、Universal Flash Storage に追加のサポートを提供するために、ufs.h ヘッダーが Windows 10 Version 1709 に追加されました。

Posix の更新には、新しい関数 **delete** と **rename** が含まれています。

Windows 10 Version 1709 で更新されたヘッダーは次のとおりです。

- ata.h
- fltKernel.h
- minitape.h
- ntddscsi.h
- ntddstor.h
- ntddvol.h
- ntifs.h
- scsi.h
- storport.h

### <a name="usb"></a>USB

USB 用のこれらの新機能は、Windows 10 バージョン1709で追加されました。

#### <a name="media-agnostic-usb-ma-usb-protocol"></a>Media Agnostic USB (MA-USB) プロトコル

USB ドライバー スタックは、Media Agnostic USB (MA-USB) プロトコルを使うことで、Wi-Fi などの非 USB 物理メディアを介して USB パケットを送信することができます。 この機能を実装するために、新しいプログラミング インターフェイスがリリースされています。 ドライバーは、この新しい DDI により、[_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays) に関連付けられている遅延を判断することができます。 この情報を取得するには、新しい URB 要求を作成します。
この新機能については、次のトピックをご覧ください。

- [Media-Agnostic (MA-USB) 用 USB クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-client-drivers-for-ma-usb)
- [_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays)
- [USB 要求ブロック (URB)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/communicating-with-a-usb-device)

MA-USB をサポートするには、ホスト コントローラーのドライバーが特定のコールバック関数を実装することでトランスポートの特性を提供する必要があります。 次の表は、MA-USB をサポートするコールバック関数と構造体を示しています。

| コールバック関数 | 構造 |
| ----- | ----- |
| [EVT_UCX_USBDEVICE_GET_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_get_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |
| [EVT_UCX_USBDEVICE_RESUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_resume) | [UCX_CONTROLLER_ENDPOINT_CHARACTERISTIC_PRIORITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_priority) |
| [EVT_UCX_USBDEVICE_SUSPEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_suspend) | [UCX_ENDPOINT_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_characteristic) |
| [EVT_UCX_ENDPOINT_GET_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_get_isoch_transfer_path_delays) | [UCX_ENDPOINT_CHARACTERISTIC_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_type) |
| [EVT_UCX_ENDPOINT_SET_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_set_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |

#### <a name="synchronized-system-qpc-with-usb-frame-and-microframes"></a>USB のフレームやマイクロフレームと同期するシステム QPC

フレームとマイクロフレームと同期された system query performance counter (QPC) 値を取得する新しいプログラミングインターフェイスが追加されました。

この情報は、呼び出し元がホスト コントローラーでこの機能を有効にしている場合にのみ取得されます。 この機能を有効にするには、ホスト コントローラーのドライバーで次のコールバック関数を実装する必要があります。

- [EVT_UCX_CONTROLLER_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_frame_number_and_qpc_for_time_sync)
- [EVT_UCX_CONTROLLER_START_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_start_tracking_for_time_sync)
- [EVT_UCX_CONTROLLER_STOP_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_stop_tracking_for_time_sync)

アプリケーションは、次の API を使って機能を有効または無効にし、情報を取得することができます。

- [WinUsb_GetCurrentFrameNumberAndQpc](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumberandqpc)
- [WinUsb_StartTrackingForTimeSync](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_starttrackingfortimesync)
- [WinUsb_StopTrackingForTimeSync](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_stoptrackingfortimesync)

他のドライバーは、次の IOCTL 要求を送信して機能を有効または無効にし、情報を取得することができます。

- [IOCTL_USB_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_frame_number_and_qpc_for_time_sync)
- [IOCTL_USB_START_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_start_tracking_for_time_sync)
- [IOCTL_USB_STOP_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_stop_tracking_for_time_sync)

これらのサポート構造は、USB フレームとマイクロフレームを使用して同期されたシステム OPC 用です。

- [USB_START_TRACKING_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_start_tracking_for_time_sync_information)
- [USB_STOP_TRACKING_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_stop_tracking_for_time_sync_information)
- [USB_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_frame_number_and_qpc_for_time_sync_information)

#### <a name="ioctl_ucmtcpci_port_controller_displayport_display_out_status_changed"></a>IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED

[IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmtcpciportcontrollerrequests/ni-ucmtcpciportcontrollerrequests-ioctl_ucmtcpci_port_controller_displayport_display_out_status_changed) 要求は、USB Type-C ポート コントローラー インターフェイス フレームワーク拡張機能の新しい要求です。 この要求は、DisplayPort 接続のディスプレイ出力の状態が変更されたことをクライアント ドライバーに通知します。

これらの構造体は、IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED の要求をサポートします。

- [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED_IN_PARAMS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmtcpciportcontrollerrequests/ns-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status_changed_in_params)
- [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmtcpciportcontrollerrequests/ne-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status)
