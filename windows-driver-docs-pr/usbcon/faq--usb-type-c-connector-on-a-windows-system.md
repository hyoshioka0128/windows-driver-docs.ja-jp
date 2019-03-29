---
Description: Frequently asked questions for OEMs who want to build Windows systems with USB Type-C connectors.
title: よく寄せられる質問 - Windows システム上の C-USB 型コネクタ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de24442fd628eee893fce57e08deac76308fa89b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573329"
---
# <a name="faq-usb-type-c-connector-on-a-windows-system"></a>よくあるご質問:Windows システムにおける USB Type-C コネクタ


**最終更新日**

-   2016 年 12 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

よく寄せられる型-C# の USB コネクタでの Windows システムを構築したい Oem の質問です。

-   [USB タイプ-c connector の機能](#features)
-   [オペレーティング システムがいずれかの入力をネゴシエートする必要がある代替モードにしますか?たとえば、DP 2 レーンとします。配布ポイントの 4 レーンでしょうか。](#does-the-operating-system-have-any-input-into-which-alternate-mode-needs-to-be-negotiated--for-instance--dp-2-lane-vs--dp-4-lane-)
-   [これら 2 種類 C と PD 課金のしくみ](#how-does-pre-os-charging-with-type-c-and-pd-work-)
-   [Continuum のようなドッキングのシナリオを有効にする、USB ホストがある場合に、電話を課金される方法は?](#how-can-i-charge-the-phone-when--it-is-a-usb-host--to-enable-docking-scenarios-like-continuum-)
-   [Windows 10 Mobile は、ビルボードの USB デバイスをサポートしますか。](#does-windows-10-mobile-support-usb-billboard-devices--)
-   [Windows 8.1、Windows 8、Windows 7 をサポートして USB 型-c でしょうか。](#do-windows-8-1--windows-8--windows-7-support-usb-type-c--)
-   [UCSI は Windows 8.1、Windows 8、Windows 7 でサポートされますか。](#is-ucsi-supported-on-windows-8-1--windows-8--windows-7-)
-   [UCSI の実装をテストするにはどうしますか。](#how-do-we-test-our-implementation-of-ucsi-----)
-   [正確な条件と UI のさまざまなエラーは?](#what-is-the-exact-condition-and-ui-for-the-different-errors-)
-   [PD 以外のポートが PD プロバイダーに接続されている場合に起こる逆に、PD コンシューマーが PD プロバイダーではないシステムに接続されているときの動作ですか。](#what-happens-when-a-non-pd-port-is-connected-to-pd-provider-----conversely--what-happens-when-a-pd-consumer-is-connected-to-a-system-that-is-not-a-pd-provider-----)
-   [Thunderbolt や SuperMHL、PCI express がこれらの機能をサポートしていない PC に接続されている場合に起こる](#what-happens-when-thunderbolt--supermhl--or-pci-express--is-connected-to-a-pc-that-does-not-support-those-capabilities-----)
-   [MTP 経由で USB 型-C# Windows でサポートされているとは制限はありますか。](#is--mtp-over-usb-type-c-supported-in-windows--are--there-any-limitations-)
-   [ダウン ストリーム デバイスおよびハブ接続し、USB コネクタ マネージャー (UCM) との通信方法でしょうか。](#how-do-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager--ucm------)
-   [HLK テストに USB 種類 C の MUTT が必要ですか。](#do-i-need-a-usb-type-c-mutt-for-hlk-tests-)
-   [Microsoft サポート P2P データが同じ Windows 10 SKU 間で転送するのでしょうか。](#will-microsoft-support-p2p-data-transfer-between-same-windows-10-sku-----)
-   [UCM クラスの拡張機能 (UcmCx) は、PMIC またはバッテリの充電状態を取得または設定のドライバーとで通信 PD をサポートしているクライアント ドライバーは PMIC またはバッテリのドライバーと直接通信する必要がありますか。](#does-ucm-class-extension--ucmcx--communicate-with-pmic-or-battery-driver-to-get-set-charging-status-or-does-the-client-driver-that-supports-pd-need-to-communicate-with-the-pmic-or-battery-driver-directly-----)
-   [HLK は USB 型-C# をサポートしますか。](#does-the-hlk-support-usb-type-c-----)
-   [UCSI とは何ですか。](#what-is-ucsi-)
-   [Windows 10 で UCSI 実装が正常に動作してかどうか確認方法](#how-can-we-check-if-our-ucsi-implementation-works-correctly-with-windows-10-----)
-   [Windows の要件を満たしているかどうかを確認する Windows 10 では、UCMCx クライアント ドライバーをテストする方法はありますかユーザーによって、Windows 上のテストして新機能のツールまたは方法を使用することができますか。](#how-do-i-test-my-ucmcx-client-driver-on-windows-10-to-make-sure-it-meets-windows-s-requirement--what-s-tool-or-method-can-be-used-to-test-on-windows-by-user-----)
-   [UCM クラスの拡張機能で処理操作は VBus/VConn 制御とロールから切り替えるでしょうか。または、パートナーは VBUS コントロールと USB モードの切り替えを処理するイベントのコールバック関数を実装する必要があります。](#is-vbus-vconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension--or-partner-would-need-to-implement-event-callback-function-to-handle-vbus-control-and-usb-mode-switch-----)

## <a name="usb-type-c-connector-features"></a>USB タイプ-c connector の機能


-   **対称的、および元に戻すことのデザイン**
    -   コネクタは、*対称*します。 ケーブルでは、USB 型-C# のコネクタを使用するホストと関数のデバイスを許可する各 end の型から C の USB コネクタがあります。 コネクタを比較するイメージを次に示します。
    -   コネクタは、*元に戻すこと*します。 従来のコネクタは、接続されている、「側-右上」する必要があります。 元に戻すことの設計では、コネクタを反転させることができます。

-   **すべての USB デバイス速度をサポートしています**

    コネクタは、低速、完全な高速、高速で (を含む SS +) SuperSpeed USB デバイスをサポートできます。

-   **別のモード**

    コネクタがサポートできる*モードを代替*します。 別のモードの機能は、同時に USB 2.0 の維持および機能の充電中に、USB ケーブルで実行するための USB 以外のプロトコルを使用できます。 現在、最も人気のある別のモードは、ディスプレイ ポート等/DockPort と MHL は。

    -   **DisplayPort** /**DockPort**

        この代替モードは、USB コネクタ経由で外部ディスプレイ ポート等を表示するには、オーディオ/ビデオをプロジェクトにできます。

    -   **MHL**

        MHL 代替モードはにより、ユーザーが外部プロジェクトのビデオ/オーディオ MHL をサポートするを表示します。

-   **ビルボードのエラー メッセージ**

    ユーザーが代替モードのデバイスを USB 型-C#、または接続されている PC または電話でサポートされていないアダプターを接続するデバイスまたはアダプターは問題のトラブルシューティングを行うユーザーを支援するエラー状態に関する情報を含むビルボード デバイスを公開できます。

-   **電力を制限します。**

    USB タイプ-c コネクタを持つシステムが電源上限の引き上げ、5 v、3A、15W までをサポートできます。

    さらに、コネクタをサポートできます必要に応じて、*配信の電源を*で定義されている機能、 [USB 電力配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)OEM です。 コネクタは、電源の配信をサポートする場合 USB 型-C# のシステム電源のソース プロバイダーとコンシューマーでき台の 100 w までをサポートします。

-   **USB 2 つのロールをサポートします。**

    周辺機器は USB 型-C# のコネクタでは、関数から従来のモバイル システムの役割をホストに変更すると、モバイル システムに接続できます。 同じシステムが PC に接続されているし、システムは、関数の役割を再開します。 PC ホストになります。

## <a name="does-the-operating-system-have-any-input-into-which-alternate-mode-needs-to-be-negotiated-for-instance-dp-2-lane-vs-dp-4-lane"></a>オペレーティング システムがいずれかの入力をネゴシエートする必要がある代替モードにしますか? たとえば、DP 2 レーンとします。配布ポイントの 4 レーンでしょうか。


No. オペレーティング システム (または、Microsoft が提供するソフトウェア コンポーネント) には、別のモードを選択する際に一部再生されません。 コネクタは、USB コネクタ マネージャー (UCM) クライアント ドライバー具体的には、ドライバーによって決定されます。 ドライバーのハードウェア インターフェイスを使用して、コネクタのファームウェアと通信して行われます。

## <a name="how-does-pre-os-charging-with-type-c-and-pd-work"></a>これら 2 種類 C と PD 課金のしくみ


Os 起動前の課金を有効にすると、OEM によって所有されます。 実装することもできます[USB 電力配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)、料金は、オペレーティング システムを起動するまでの USB 型-c power レベルでします。

## <a name="how-can-i-charge-the-phone-when-it-is-a-usb-host-to-enable-docking-scenarios-like-continuum"></a>Continuum のようなドッキングのシナリオを有効にする、USB ホストがある場合に、電話を課金される方法は?


考慮する点を次に示します。

-   実装する必要があります[USB 電力配信](https://go.microsoft.com/fwlink/p/?LinkID=623310)電源とデータ ロールが個別に交換するしないことができます。
-   ドックのアップ ストリームのポートは、USB 型-C# 仕様で定義されている課金 UFP として実装する必要があります。 詳細については、4.8.4、バージョン 1.1 のセクションを参照してください。
-   ドックが DR を要求する必要があります\_、DFP、またはプル要求に問題を解決した場合は、スワップ\_UFP に問題を解決した場合は、スワップします。

    初期 DFP は、電源は、データのロールを変更する必要があります。 初期 UFP は、電源シンク power ロールを変更する必要があります。 これらのコールバック関数の実装では、これらの操作を実行できます。

## <a name="does-windows10-mobile-support-usb-billboard-devices"></a>Windows 10 Mobile は、ビルボードの USB デバイスをサポートしますか。


はい、に従って、USB ビルボードをサポートするデバイスに電話を接続する場合、[ビルボード デバイス仕様の USB デバイス クラス定義](https://go.microsoft.com/fwlink/p/?linkid=620207)ユーザーに通知されます。 USB コネクタ マネージャー (UCM) クライアント ドライバーは、通知を処理する必要はありません。 システムで、代替のモードが認識されない場合は、モードを入力しないでください。

## <a name="do-windows81-windows8-windows7-support-usb-type-c"></a>Windows 8.1、Windows 8、Windows 7 をサポートして USB 型-c でしょうか。


No. USB タイプ-C は Windows 10 以前の Windows のバージョンではサポートされていません。

## <a name="is-ucsi-supported-on-windows81-windows8-windows7"></a>UCSI は Windows 8.1、Windows 8、Windows 7 でサポートされますか。


No. UCSI は Windows 10 以前の Windows のバージョンでサポートされていません。

## <a name="how-do-we-test-our-implementation-of-ucsi"></a>UCSI の実装をテストするにはどうしますか。


実装をテストするで指定されたガイドラインに従って[USB 型-c 手動の相互運用性のテスト手順](type.md)します。 Windows 10 用 Windows ハードウェア ラボ キット (HLK) USB テストを実行することをお勧めします。 これらのテストが記載されて[USB の Windows ハードウェア認定キット テスト](windows-hardware-certification-kit-tests-for-usb.md)します。

## <a name="what-is-the-exact-condition-and-ui-for-the-different-errors"></a>正確な条件と UI のさまざまなエラーは?


Windows 10 では、USB 型-C# のハードウェアとソフトウェアのさまざまな組み合わせでの制限事項についてユーザーを教育する USB 型から C のエラー メッセージのセットを表示できます。 たとえば、ユーザーが「デバイスが充電緩やかに変化」充電器は、型-C# の USB コネクタに接続されている場合はメッセージが十分に強力で、システムと互換性がないまたは充電中以外のポートに接続されているを取得する可能性があります。 詳細については、次を参照してください。 [USB 型 C Windows システムのメッセージのトラブルシューティングを行う](https://go.microsoft.com/fwlink/?LinkId=526894)します。

## <a name="what-happens-when-a-non-pd-port-is-connected-to-pd-provider-conversely-what-happens-when-a-pd-consumer-is-connected-to-a-system-that-is-not-a-pd-provider"></a>PD 以外のポートが PD プロバイダーに接続されている場合に起こる 逆に、PD コンシューマーが PD プロバイダーではないシステムに接続されているときの動作ですか。


PD 以外のポートが USB 型-C# の現在のレベルを使用して、システムを請求しようとするとします。 詳細については、次を参照してください。 [USB 3.1 と USB 型-C# 仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)します。

## <a name="what-happens-when-thunderbolt-supermhl-or-pci-express-is-connected-to-a-pc-that-does-not-support-those-capabilities"></a>Thunderbolt や SuperMHL、PCI express がこれらの機能をサポートしていない PC に接続されている場合に起こる


代替モード機能では、同時に USB 2.0 の維持および機能の充電中に、USB ケーブルで実行するため (Thunderbolt、SuperMHL) などの USB 以外のプロトコルを使用できます。 ユーザーは、USB 型-c 代替モードのデバイスまたは接続されている PC または Windows 10 を実行している電話でサポートされていないアダプターを接続する場合は、エラー条件が検出され、ユーザーにメッセージが表示されます。

-   デバイスまたはアダプターは、ビルボードのデバイスを公開する場合、ユーザーには、問題をトラブルシューティングを行うのに役立つエラー条件についての情報が表示されます。 Windows 10 では、ビルボードのデバイスに、インボックス ドライバーを提供し、ユーザー エラーが発生したことを通知します。
-   ユーザーは、エラー通知が表示される、「USB 接続の改善を試してください」可能性があります。 詳細については、次を参照してください。 [USB 型 C Windows システムのエラー メッセージ](introduction-to-usb-type-c-connectors.md#-4)します。

最適な結果を PC または電話ケーブルで別のモードのデバイスまたはアダプターの要件を満たしていることを確認します。

## <a name="is-mtp-over-usb-type-c-supported-in-windows-are-there-any-limitations"></a>MTP 経由で USB 型-C# Windows でサポートされているとは 何らかの制限はありますか。


Windows 10 デスクトップ エディションの場合は、開始側のロールで MTP をサポートしていますWindows 10 Mobile では、応答側ロールの MTP をサポートします。

## <a name="how-do-downstream-devices-and-hubs-connect-and-communicate-with-usb-connector-manager-ucm"></a>ダウン ストリーム デバイスおよびハブ接続し、USB コネクタ マネージャー (UCM) との通信方法でしょうか。


UCM は独自のデバイス スタック (を参照してください[アーキテクチャ。Windows システムの USB 型-C# のデザイン](architecture--usb-type-c-in-a-windows-system.md))。 Windows 10 のサポート USB 型-C# にはには、別のクラス ドライバーが、さまざまな種類 C の USB コネクタと通信する方法を知っているかどうかを確認する必要なプラミングが含まれます。 USB 型-C# の Windows 10 のサポートを取得するためには、UCM デバイス スタックをプラグインする必要があります。

## <a name="do-i-need-a-usb-type-c-mutt-for-hlk-tests"></a>HLK テストに USB 種類 C の MUTT が必要ですか。


Windows 10 用 Windows HLK には、USB ホストと関数のコント ローラーのテストが含まれています。 システムをテストするには、C A USB アダプターを使用します。 これらのテストが記載されて[USB の Windows ハードウェア認定キット テスト](windows-hardware-certification-kit-tests-for-usb.md)します。

## <a name="will-microsoft-support-p2p-data-transfer-between-same-windows10-sku"></a>Microsoft サポート P2P データが同じ Windows 10 SKU 間で転送するのでしょうか。


これは、有効な接続ではありません。

-   デスクトップ エディションの Windows 10 を実行している 2 つの Pc に接続することはできません。
-   Windows 10 Mobile を実行している 2 つのモバイル デバイスを接続することはできません。

ユーザーがこのような接続を確立しようとすると、Windows では、エラー メッセージが表示されます。 詳細については、次を参照してください。 [USB 型 C Windows システムのエラー メッセージ](introduction-to-usb-type-c-connectors.md#-6)します。

Windows Mobile デバイスと Windows デスクトップ デバイスの間の唯一の有効な接続です。

## <a name="does-ucm-class-extension-ucmcx-communicate-with-pmic-or-battery-driver-to-getset-charging-status-or-does-the-client-driver-that-supports-pd-need-to-communicate-with-the-pmic-or-battery-driver-directly"></a>UCM クラスの拡張機能 (UcmCx) は、PMIC またはバッテリの充電状態を取得または設定のドライバーとで通信 PD をサポートしているクライアント ドライバーは PMIC またはバッテリのドライバーと直接通信する必要がありますか。


ソフトウェア支援型のプラットフォームに充電 UcmCx が PMIC およびバッテリ サブシステムと通信します。 クライアント ドライバーは、ハードウェア インターフェイスを通じて、ハードウェアと通信することで、課金レベルを判断します。 ハードウェア依存のプラットフォームでは、埋め込みコント ローラーは充電責任を負います。 UcmCx には、プロセスの一部はありません。

## <a name="does-the-hlk-support-usb-type-c"></a>HLK は USB 型-C# をサポートしますか。


Windows HLK の Windows 10 では、USB 型-C# の特定のテストはありません。 Windows 10 用 Windows HLK で USB テストを実行することをお勧めします。 これらのテストが記載されて[USB の Windows ハードウェア認定キット テスト](windows-hardware-certification-kit-tests-for-usb.md)します。

## <a name="what-is-ucsi"></a>UCSI とは何ですか。


USB タイプ C コネクタ システム ソフトウェア インターフェイス (UCSI) 仕様は、USB 型 C コネクタ システム ソフトウェア インターフェイス (UCSI) の機能について説明し、ハードウェア コンポーネントの設計者、システム ビルダー、レジスタとデータの構造を説明しますデバイス ドライバー開発者向け。 取得、仕様から[このサイト](https://go.microsoft.com/fwlink/p/?LinkId=703713)します。

Microsoft では、Windows、UcmUcsi.sys、仕様で定義されている機能を実装すると、インボックス ドライバーを提供します。 このドライバーは、埋め込みコント ローラーのシステムを対象としています。

## <a name="how-can-we-check-if-our-ucsi-implementation-works-correctly-with-windows10"></a>Windows 10 で UCSI 実装が正常に動作してかどうか確認方法


Windows 10 用 Windows HLK で USB テストを実行することをお勧めします。 これらのテストが記載されて[USB の Windows ハードウェア認定キット テスト](windows-hardware-certification-kit-tests-for-usb.md)します。

## <a name="how-do-i-test-my-ucmcx-client-driver-on-windows10-to-make-sure-it-meets-windowss-requirement-whats-tool-or-method-can-be-used-to-test-on-windows-by-user"></a>Windows の要件を満たしているかどうかを確認する Windows 10 では、UCMCx クライアント ドライバーをテストする方法はありますか ユーザーによって、Windows 上のテストして新機能のツールまたは方法を使用することができますか。


Windows 10 用 Windows HLK で USB テストを実行することをお勧めします。 これらのテストが記載されて[USB の Windows ハードウェア認定キット テスト](windows-hardware-certification-kit-tests-for-usb.md)します。

## <a name="is-vbusvconn-control-and-role-switch-operations-handled-by-the-ucm-class-extension-or-partner-would-need-to-implement-event-callback-function-to-handle-vbus-control-and-usb-mode-switch"></a>UCM クラスの拡張機能で処理操作は VBus/VConn 制御とロールから切り替えるでしょうか。 または、パートナーは VBUS コントロールと USB モードの切り替えを処理するイベントのコールバック関数を実装する必要があります。


UCM クラスの拡張機能は、コネクタのデータまたは電源の方向を変更するオペレーティング システムから要求を取得する可能性があります。 クライアント ドライバーの実装を呼び出すときに、それらの要求を取得、 [ *EVT\_UCM\_コネクタ\_設定\_データ\_ロール*](https://msdn.microsoft.com/library/windows/hardware/mt187818)と[ *EVT\_UCM\_コネクタ\_設定\_POWER\_ロール*](https://msdn.microsoft.com/library/windows/hardware/mt187819)コールバック関数 (場合、コネクタPD を実装)。 実装では、クライアント ドライバーが必要なコントロール、VBUS と VCONN pin です。 これらのコールバック関数の詳細については、次を参照してください。[型-C# の USB コネクタ ドライバー](bring-up-a-usb-type-c-connector-on-a-windows-system.md)します。

 

 




