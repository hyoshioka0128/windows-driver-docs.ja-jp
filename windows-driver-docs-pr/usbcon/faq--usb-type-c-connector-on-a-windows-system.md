---
Description: USB タイプ C コネクタを使用して Windows システムを構築する必要がある Oem 向けのよく寄せられる質問。
title: FAQ-Windows システムでの USB タイプ-C コネクタ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec045e2702731f2542d91625d4b2f56c4d880466
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845005"
---
# <a name="faq-usb-type-c-connector-on-a-windows-system"></a>FAQ: Windows システムでの USB タイプ C コネクタ

**Windows のバージョン**:

* Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
* Windows 10 Mobile

USB タイプ C コネクタを使用して Windows システムを構築する必要がある Oem 向けの一般的な説明です。

* [USB タイプ-C コネクタの機能](#usb-type-c-connector-features)
* [代替モードのネゴシエートが必要なオペレーティングシステム入力 (DP 2-lane と DP 4-lane など)](#operating-system-input-into-which-alternate-mode-needs-to-be-negotiated-such-as-dp-2-lane-vs-dp-4-lane)
* [タイプ C と PD による OS の課金](#pre-os-charging-with-type-c-and-pd)
* [デバイスが USB ホストである場合に電話を請求して、連続性のようなドッキングシナリオを有効にする](#charging-the-phone-when-it-is-a-usb-host-to-enable-docking-scenarios-like-continuum)
* [Windows 10 Mobile の USB ビルボードデバイスのサポート](#windows10-mobile-support-of-usb-billboard-devices)
* [以前のバージョンの Windows での USB タイプ C のサポート](#support-for-usb-type-c-on-earlier-versions-of-windows)
* [以前のバージョンの Windows での UCSI のサポート](#ucsi-support-on-earlier-versions-of-windows)
* [UCSI の実装をテストする方法](#how-to-test-an-implementation-of-ucsi)
* [さまざまなエラーの条件と UI](#conditions-and-ui-for-the-different-errors)
* [Pd 以外のポートを pd プロバイダーに接続し、pd コンシューマーを pd プロバイダーではないシステムに接続する](#connecting-a-non-pd-port-to-a-pd-provider-and-a-pd-consumer-to-a-system-that-is-not-a-pd-provider)
* [Thunderbolt icon、SuperMHL、または PCI express を、これらの機能をサポートしていない PC に接続する](#connecting-thunderbolt-supermhl-or-pci-express-to-a-pc-that-does-not-support-those-capabilities)
* [Windows での USB タイプ C 経由の MTP のサポートと制限](#support-and-limitations-for-mtp-over-usb-type-c-in-windows)
* [ダウンストリームデバイスとハブが USB コネクタマネージャー (UCM) に接続して通信する方法](#how-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager-ucm)
* [HLK テストの USB タイプ-C MUTT の要件](#usb-type-c-mutt-requirements-for-hlk-tests)
* [Microsoft では、同じ Windows 10 SKU 間での P2P データ転送をサポートしています](#microsoft-support-for-p2p-data-transfer-between-the-same-windows10-sku)
* [UCM クラス拡張 (UcmCx) と PMIC またはバッテリドライバーとの通信による充電状態の取得/設定](#ucm-class-extension-ucmcx-communication-with-pmic-or-battery-driver-to-getset-charging-status)
* [HLK USB タイプのサポート-C](#hlk-support-for-usb-type-c)
* [UCSI](#ucsi)
* [Windows 10 で実行されている UCSI 実装をテストする](#test-a-ucsi-implementation-running-on-windows-10)
* [Windows 10 で UCMCx クライアントドライバーをテストする](#test-a-ucmcx-client-driver-on-windows-10)
* [UCM クラス拡張によって処理される VBus/Vbus 制御とロールスイッチ操作](#vbusvconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension)

## <a name="usb-type-c-connector-features"></a>USB タイプ-C コネクタの機能

### <a name="symmetric-and-reversible-design"></a>対称および元に戻すことが可能な設計

* コネクタは*対称*です。 ケーブルには、各エンドで USB タイプの C コネクタがあり、ホストと機能デバイスで USB タイプ C コネクタを使用できます。 コネクタを比較するイメージを次に示します。
* コネクタは、元に*戻す*ことができるように設計されています。 従来のコネクタは、"右側の" 側に接続する必要がありました。 元に戻せる設計では、コネクタを反転させることができます。

### <a name="supports-all-usb-device-speeds"></a>すべての USB デバイスの速度をサポートする

コネクタは、低速、高速、高速、SuperSpeed (SS + を含む) の USB デバイスをサポートできます。

### <a name="alternate-modes"></a>代替モード

コネクタは、*代替モード*をサポートできます。 代替モード機能を使用すると、usb ケーブル上で非 USB プロトコルを実行できます。同時に、usb 2.0 と充電の機能を維持できます。 現在、最も一般的な代替モードは DisplayPort/DockPort と MHL です。

* **DisplayPort** /**DockPort**

  この代替モードでは、ユーザーは、USB コネクタ経由で外部 DisplayPort を表示することができます。

* **MHL**

  MHL の代替モードでは、ユーザーは MHL をサポートする外部ディスプレイにビデオ/オーディオを投影できます。

* **ビルボードのエラーメッセージ**

  接続されている PC または電話でサポートされていない USB タイプ C 代替モードデバイスまたはアダプターをユーザーが接続すると、デバイスまたはアダプターは、ユーザーが問題をトラブルシューティングするのに役立つエラー状態に関する情報を含むビルボードデバイスを公開できます。

* **電力制限の向上**

   USB タイプ C コネクタを使用するシステムでは、電力制限が高く、最大5V、3A、15W がサポートされています。

   また、コネクタは、 [USB 電力配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)の OEM によって定義されているように、必要に応じて、*電力配信*機能をサポートすることもできます。 コネクタが電力の配信をサポートしている場合は、USB タイプ C システムを電源供給プロバイダーまたはコンシューマーとして使用し、最大100W をサポートできます。

* **USB デュアルロールのサポート**

  周辺機器は、USB タイプ C コネクタを使用してモバイルシステムに接続し、モバイルシステムの従来の役割を機能からホストに変更することができます。 同じシステムが PC に接続されている場合、システムは機能の役割を再開し、PC はホストになります。

## <a name="operating-system-input-into-which-alternate-mode-needs-to-be-negotiated-such-as-dp-2-lane-vs-dp-4-lane"></a>代替モードのネゴシエートが必要なオペレーティングシステム入力 (DP 2-lane と DP 4-lane など)

いいえ。 オペレーティングシステム (または Microsoft が提供するすべてのソフトウェアコンポーネント) は、代替モードの選択には含まれません。 この決定は、コネクタのドライバー (具体的には、USB コネクタマネージャー (UCM) クライアントドライバーによって行われます。 ドライバーは、ハードウェアインターフェイスを使用してコネクタのファームウェアと通信することによってこれを行います。

## <a name="pre-os-charging-with-type-c-and-pd"></a>タイプ C と PD による OS の課金

プレ OS 課金の有効化は、OEM によって所有されています。 [Usb 電力配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)を実装しないように選択することも、オペレーティングシステムを起動するまで Usb タイプ C の電源レベルで課金することもできます。

## <a name="charging-the-phone-when-it-is-a-usb-host-to-enable-docking-scenarios-like-continuum"></a>デバイスが USB ホストである場合に電話を請求して、連続性のようなドッキングシナリオを有効にする

次に、考慮すべき点をいくつか示します。

* 電源とデータの役割を個別に交換できるように、 [USB 電源配布](https://go.microsoft.com/fwlink/p/?LinkID=623310)を実装する必要があります。
* Dock のアップストリームポートは、USB タイプ C 仕様で定義されている充電 UFP として実装する必要があります。 詳細については、セクション4.8.4、バージョン1.1 を参照してください。
* DFP に解決された場合、dock は DR\_スワップを要求する必要があります。または、UFP に解決された場合は、PR\_スワップします。

  最初の DFP は電源であるため、データの役割を変更する必要があります。 初期 UFP は電源シンクなので、電源ロールを変更する必要があります。 これらの操作は、次のコールバック関数の実装で実行できます。

## <a name="windows10-mobile-support-of-usb-billboard-devices"></a>Windows 10 Mobile の USB ビルボードデバイスのサポート

はい。スマートフォンを、[ビルボードデバイス仕様の Usb デバイスクラス定義](https://go.microsoft.com/fwlink/p/?linkid=620207)に従って、usb ビルボードをサポートするデバイスに接続すると、ユーザーに通知されます。 USB コネクタマネージャ (UCM) クライアントドライバは、通知を処理する必要がありません。 システムで代替モードが認識されない場合は、モードには入りません。

## <a name="support-for-usb-type-c-on-earlier-versions-of-windows"></a>以前のバージョンの Windows での USB タイプ C のサポート

USB タイプ C は、Windows 10 より前のバージョンの Windows ではサポートされていません。

## <a name="ucsi-support-on-earlier-versions-of-windows"></a>以前のバージョンの Windows での UCSI のサポート

UCSI は、Windows 10 より前のバージョンの Windows ではサポートされていません。

## <a name="how-to-test-an-implementation-of-ucsi"></a>UCSI の実装をテストする方法

実装をテストするには、 [USB タイプ C の手動による相互運用性のテスト手順](type.md)に関するガイドラインに従ってください。 Windows 10 用 Windows ハードウェアラボキット (HLK) で USB テストを実行することをお勧めします。 これらのテストは、「 [Windows ハードウェア認定キットの USB 用テスト](windows-hardware-certification-kit-tests-for-usb.md)」に記載されています。

## <a name="conditions-and-ui-for-the-different-errors"></a>さまざまなエラーの条件と UI

Windows 10 では、usb タイプ C のハードウェアとソフトウェアのさまざまな組み合わせによる制限事項についてユーザーを教育するのに役立つ、一連の USB タイプ C エラーメッセージを表示できます。 たとえば、USB タイプ C コネクタに接続されているチャージャーが十分ではない場合、システムとの互換性がない場合、または充電ポート以外に接続されている場合、ユーザーは "デバイスが充電されています" というメッセージが表示されることがあります。 詳細については、「 [USB タイプ-C Windows システムのメッセージのトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=526894)」を参照してください。

## <a name="connecting-a-non-pd-port-to-a-pd-provider-and-a-pd-consumer-to-a-system-that-is-not-a-pd-provider"></a>Pd 以外のポートを pd プロバイダーに接続し、pd コンシューマーを pd プロバイダーではないシステムに接続する

非 PD ポートは、USB タイプ C の現在のレベルを使用してシステムの課金を試行します。 詳細については、「 [usb 3.1 および Usb C 仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)」を参照してください。

## <a name="connecting-thunderbolt-supermhl-or-pci-express-to-a-pc-that-does-not-support-those-capabilities"></a>Thunderbolt icon、SuperMHL、または PCI express を、これらの機能をサポートしていない PC に接続する

代替モード機能を使用すると、usb ケーブル上で非 USB プロトコル (Thunderbolt icon、SuperMHL など) を実行できます。同時に、usb 2.0 と充電の機能が維持されます。 接続されている PC または Windows 10 を実行している電話でサポートされていない USB タイプ C 代替モードデバイスまたはアダプターをユーザーが接続すると、エラー状態が検出され、ユーザーにメッセージが表示されます。

* デバイスまたはアダプターがビルボードデバイスを公開すると、問題のトラブルシューティングに役立つエラー状態に関する情報が表示されます。 Windows 10 は、ビルボードデバイス用にインボックスドライバーを提供し、エラーが発生したことをユーザーに通知します。
* "USB 接続を改善してみてください" というエラー通知がユーザーに表示される場合があります。 詳細については、「 [USB タイプ-C Windows システムのエラーメッセージ](introduction-to-usb-type-c-connectors.md#-4)」を参照してください。

最適な結果を得るには、代替モードのデバイスまたはアダプターの要件が PC または電話またはケーブルによって満たされていることを確認してください。

## <a name="support-and-limitations-for-mtp-over-usb-type-c-in-windows"></a>Windows での USB タイプ C 経由の MTP のサポートと制限

Windows 10 for desktop エディションでは、開始側ロールで MTP がサポートされています。Windows 10 Mobile では、応答側ロールで MTP がサポートされています。

## <a name="how-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager-ucm"></a>ダウンストリームデバイスとハブが USB コネクタマネージャー (UCM) に接続して通信する方法

UCM は独自のデバイススタックです (「[アーキテクチャ: Windows システム向けの USB タイプ C 設計](architecture--usb-type-c-in-a-windows-system.md)」を参照してください)。 USB タイプ C の Windows 10 のサポートには、さまざまなクラスドライバーが異なる種類の USB (C) コネクタと通信する方法を認識できるようにするために必要な構成要素が含まれています。 USB タイプ C の Windows 10 サポートを利用するには、UCM デバイススタックにプラグインする必要があります。

## <a name="usb-type-c-mutt-requirements-for-hlk-tests"></a>HLK テストの USB タイプ-C MUTT の要件

Windows 10 用の windows HLK には、USB ホストと機能コントローラーのテストが含まれています。 システムをテストするには、USB C アダプターを使用します。 これらのテストは、「 [Windows ハードウェア認定キットの USB 用テスト](windows-hardware-certification-kit-tests-for-usb.md)」に記載されています。

## <a name="microsoft-support-for-p2p-data-transfer-between-the-same-windows10-sku"></a>Microsoft では、同じ Windows 10 SKU 間での P2P データ転送をサポートしています

これは有効な接続ではありません。

* Windows 10 を実行する2台の Pc をデスクトップエディションとして接続することはできません。
* Windows 10 Mobile を実行している2つのモバイルデバイスを接続することはできません。

ユーザーがこのような接続を試みると、エラーメッセージが表示されます。 詳細については、「 [USB タイプ-C Windows システムのエラーメッセージ](introduction-to-usb-type-c-connectors.md#-6)」を参照してください。

有効な接続は、Windows Mobile デバイスと Windows デスクトップデバイスの間のみです。

## <a name="ucm-class-extension-ucmcx-communication-with-pmic-or-battery-driver-to-getset-charging-status"></a>UCM クラス拡張 (UcmCx) と PMIC またはバッテリドライバーとの通信による充電状態の取得/設定

ソフトウェア支援型の課金プラットフォームでは、UcmCx は PMIC とバッテリサブシステムと通信します。 クライアントドライバーは、ハードウェアインターフェイスを介してハードウェアと通信することによって、充電レベルを決定する場合があります。 ハードウェア支援型のプラットフォームでは、埋め込みコントローラーは課金を担当します。 UcmCx はプロセスに含まれません。

## <a name="hlk-support-for-usb-type-c"></a>HLK USB タイプのサポート-C

Windows 10 用 Windows HLK では、USB タイプ C 固有のテストはありません。 Windows HLK for Windows 10 では、USB テストを実行することをお勧めします。 これらのテストは、「 [Windows ハードウェア認定キットの USB 用テスト](windows-hardware-certification-kit-tests-for-usb.md)」に記載されています。

## <a name="ucsi"></a>UCSI

USB タイプ-C コネクタシステムソフトウェアインターフェイス (UCSI) 仕様には、USB タイプ C コネクタシステムソフトウェアインターフェイス (UCSI) の機能が記述されています。また、ハードウェアコンポーネントデザイナー、システムビルダー、およびデバイスドライバーの開発者。 [このサイト](https://go.microsoft.com/fwlink/p/?LinkId=703713)から仕様を取得します。

Microsoft では、仕様で定義されている機能を実装するインボックスドライバー (UcmUcsi) を提供しています。 このドライバーは、コントローラーが組み込まれているシステムを対象としています。

## <a name="test-a-ucsi-implementation-running-on-windows-10"></a>Windows 10 で実行されている UCSI 実装をテストする

Windows HLK for Windows 10 では、USB テストを実行することをお勧めします。 これらのテストは、「 [Windows ハードウェア認定キットの USB 用テスト](windows-hardware-certification-kit-tests-for-usb.md)」に記載されています。

## <a name="test-a-ucmcx-client-driver-on-windows-10"></a>Windows 10 で UCMCx クライアントドライバーをテストする

Windows HLK for Windows 10 では、USB テストを実行することをお勧めします。 これらのテストは、「 [Windows ハードウェア認定キットの USB 用テスト](windows-hardware-certification-kit-tests-for-usb.md)」に記載されています。

## <a name="vbusvconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension"></a>UCM クラス拡張によって処理される VBus/Vbus 制御とロールスイッチ操作

UCM クラスの拡張機能は、オペレーティングシステムから、コネクタのデータまたは電源の方向を変更する要求を受け取る場合があります。 これらの要求を取得すると、クライアントドライバーの[ *.evt\_UCM\_コネクタの実装が呼び出され\_\_データ\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_data_role)および[ *.evt\_UCM\_コネクタ\_設定され\_電力\_ロール*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmmanager/nc-ucmmanager-evt_ucm_connector_set_power_role)コールバック関数 (コネクタが PD を実装している場合)。 実装では、クライアントドライバーは VBUS ピンと VBUS pin を制御する必要があります。 これらのコールバック関数の詳細については、「 [Write a USB Type-C コネクタ driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)」を参照してください。
