---
title: 通信事業者のハードウェアの概要
description: 通信事業者のハードウェアの概要
ms.assetid: b2322972-16be-443f-b46a-7834b4d7ead0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1756eea8d89dda07b8ad7ac51fdc3b7aade790a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838296"
---
# <a name="mobile-operator-hardware-overview"></a>通信事業者のハードウェアの概要


このトピックを使用して、Windows 8、Windows 8.1、および Windows 10 mobile のブロードバンドハードウェア要件と推奨事項についての概要を把握する必要があります。 以下のことをお勧めします。これにより、お客様は、簡単な接続エクスペリエンスを提供できるだけでなく、メンテナンスとサポートのコストを削減できます。

-   USB インターフェイスを提供する Embedded モバイルブロードバンドモジュールは、Windows 8、Windows 8.1、または Windows 10 ハードウェア認定の要件を満たし、モバイルブロードバンドクラスドライバーを使用して管理する必要があります。 Ihv のハードウェア要件のドキュメントでは、モバイルブロードバンドデバイスが Windows 8、Windows 8.1、または Windows 10 デバイス認定に合格する必要があります。

-   外部 USB モバイルブロードバンドドングルは、id のモーフィングをサポートする必要があります。 Ihv 向けのハードウェア要件のドキュメントでは、外部モバイルブロードバンドデバイスが Windows 8 デバイス認定、Windows 8.1、または Windows 10 デバイス認定の両方に合格し、Windows 7 ロゴ認定を受け渡す必要があります。

    -   Windows 10 コンピューターでは、ドングルは Windows 10 認定モバイルデバイスとして、モバイルブロードバンドクラスドライバーを使用して管理されます。

    -   Windows 8.1 コンピューターでは、ドングルは Windows 8.1 認定されたモバイルブロードバンドデバイスとして表示され、モバイルブロードバンドクラスドライバーを使用して管理されます。

    -   Windows 8 コンピューターでは、ドングルは Windows 8 認定モバイルデバイスとして、モバイルブロードバンドクラスドライバーを使用して管理されます。

    -   Windows 7 コンピューターでは、ドングルは大容量記憶装置として表示され、ユーザーは特定のデバイスドライバーをインストールできます。

-   EAP-SIM、USSD、または複数の PDP 接続が必要な場合は、IHV がそれを有効にする必要があります。また、Windows 8、Windows 8.1、または Windows 10 のハードウェア認定要件に準拠している必要があります。

-   ユーザーまたは IHV が必要とするその他の機能は、デバイスサービス拡張機能を使用して実装し、Windows 8、Windows 8.1、または Windows 10 でモバイルブロードバンドクラスドライバーとデバイスサービス Api を使用して有効にする必要があります。 ハードウェア要件のドキュメントの一部として、追加の機能を含める必要があります。

## <a name="span-idkey_scenariosspanspan-idkey_scenariosspanspan-idkey_scenariosspankey-scenarios"></a><span id="Key_scenarios"></span><span id="key_scenarios"></span><span id="KEY_SCENARIOS"></span>主要なシナリオ


### <a name="span-idpurchase_an_external_devicespanspan-idpurchase_an_external_devicespanspan-idpurchase_an_external_devicespanpurchase-an-external-device"></a><span id="Purchase_an_external_device"></span><span id="purchase_an_external_device"></span><span id="PURCHASE_AN_EXTERNAL_DEVICE"></span>外部デバイスを購入する

外部デバイスは、ユーザーが使用を開始する直前に挿入される可能性があります。

1.  デバイスが挿入されるとすぐに、モバイルブロードバンドクラスドライバーによって認識および管理されます。

2.  モバイルブロードバンドサービスは、IMSI を読み取り、一連のハッシュを生成します。

3.  ユーザーが **[接続]** をクリックすると、これらのハッシュを使用して、 [COSA/APN データベースの送信](cosa-apn-database-submission.md)内の接続設定が照合されます。

    -   接続に成功し、インターネット接続が利用可能な場合は、それ以上の処理は行われません。 ユーザーは既にサービスを購入しています。

    -   接続に成功しても、インターネット接続が利用できない場合は、APN データベースまたは UWP モバイルブロードバンドアプリで指定された URL が web ブラウザーに表示されます。

    -   接続に失敗した場合、ユーザーにはエラーが通知されます。

4.  ユーザーは、web サイトまたはモバイルブロードバンドアプリを使用して、サービスを購入できます。

5.  購入したデバイスは、プロビジョニングファイルからプロビジョニング API を使用してプロビジョニングされます。 プロビジョニングファイルは、web サイトまたはモバイルブロードバンドアプリによってプロビジョニングエージェントに渡されます。 プロビジョニングファイルは、ユーザーが購入したプランに関する基本情報を使用して Windows を構成します。 ネットワーク構造によっては、次のいずれかが発生します。

    -   現在の接続では、ユーザーにインターネットアクセスが許可されます。

    -   プロビジョニングファイルには、同じネットワークまたは別のネットワークに接続を切断して再接続するための手順が含まれています。これにより、インターネットアクセスが提供されます。

### <a name="span-idconnect_an_external_device_with_an_active_simspanspan-idconnect_an_external_device_with_an_active_simspanspan-idconnect_an_external_device_with_an_active_simspanconnect-an-external-device-with-an-active-sim"></a><span id="Connect_an_external_device_with_an_active_SIM"></span><span id="connect_an_external_device_with_an_active_sim"></span><span id="CONNECT_AN_EXTERNAL_DEVICE_WITH_AN_ACTIVE_SIM"></span>外部デバイスをアクティブな SIM に接続する

アクティブな SIM が既に割り当てられているアクティブなデバイスが接続されている場合、そのワークフローは、外部デバイスを購入した場合と似ています。ただし、接続しようとすると、インターネットが使用されます。 サービスを購入するには、web サイトまたはモバイルブロードバンドアプリにユーザーを指示する必要はありません。

1.  デバイスが挿入されるとすぐに、モバイルブロードバンドクラスドライバーによって認識および管理されます。

2.  モバイルブロードバンドサービスは、IMSI を読み取り、一連のハッシュを生成します。

3.  ユーザーが **[接続]** をクリックすると、これらのハッシュを使用して、 [COSA/APN データベースの送信](cosa-apn-database-submission.md)内の接続設定が照合されます。 アクティブな SIM を持つデバイスの場合、接続は成功し、インターネット接続が可能です。

## <a name="span-idcomponentsspanspan-idcomponentsspanspan-idcomponentsspancomponents"></a><span id="Components"></span><span id="components"></span><span id="COMPONENTS"></span>コンポーネント


### <a name="span-idwindows_8__windows_81__or_windows_10_certified_mobile_broadband_devicesspanspan-idwindows_8__windows_81__or_windows_10_certified_mobile_broadband_devicesspanspan-idwindows_8__windows_81__or_windows_10_certified_mobile_broadband_devicesspanwindows8-windows81-or-windows10-certified-mobile-broadband-devices"></a><span id="Windows_8__Windows_8.1__or_Windows_10_certified_mobile_broadband_devices"></span><span id="windows_8__windows_8.1__or_windows_10_certified_mobile_broadband_devices"></span><span id="WINDOWS_8__WINDOWS_8.1__OR_WINDOWS_10_CERTIFIED_MOBILE_BROADBAND_DEVICES"></span>Windows 8、Windows 8.1、または Windows 10 認定を受けたモバイルブロードバンドデバイス

Windows mobile ブロードバンドプラットフォームを最大限に活用するには、モバイルブロードバンドデバイスが Windows 8、Windows 8.1、または Windows 10 のハードウェア認定要件を満たしている必要があります。 ハードウェア認定の要件の包括的な説明については、「 [Windows ハードウェア認定の要件](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/)」を参照してください。

エンドユーザーにとって最も単純な接続エクスペリエンスは、USB ベースのモバイルブロードバンドデバイスと共に提供されます。 ハードウェア認定の要件の一部として、USB デバイスとして使用されるすべてのモバイルブロードバンドデバイスは、[モバイルブロードバンドインターフェイスモデル (mbim) 仕様](https://docs.microsoft.com/windows-hardware/drivers/network/mb-interface-model)と mbim V1.0 のエラッタに準拠している必要があります。 これには、USB インターフェイスを提供する外部 USB ドングルと埋め込みモジュールの両方が含まれます。 このクラスのデバイスでは、Windows 8、Windows 8.1、または Windows 10 にモバイルブロードバンドクラスドライバーが含まれています。これにより、IHV からの追加ドライバーが不要になり、ユーザーの接続エクスペリエンスが簡単になります。 USB およびドライバーモデル以外のハードウェアは、Windows 8、Windows 8.1、および Windows 10 認定を受け取ることができ、Microsoft Store モバイルブロードバンドアプリエクスペリエンスを提供しますが、これらはモバイルブロードバンドクラスドライバーではサポートされていません。

### <a name="span-idmobile_broadband_class_driverspanspan-idmobile_broadband_class_driverspanspan-idmobile_broadband_class_driverspanmobile-broadband-class-driver"></a><span id="Mobile_broadband_class_driver"></span><span id="mobile_broadband_class_driver"></span><span id="MOBILE_BROADBAND_CLASS_DRIVER"></span>モバイルブロードバンドクラスドライバー

モバイルブロードバンドクラスドライバーを使用すると、デバイスの製造元が特定のモバイルブロードバンドデバイス用のカスタムドライバーを提供する負担が軽減されます。 モバイルブロードバンドクラスドライバーは、Windows 8、Windows 8.1、または Windows 10 デバイス認定を満たす USB MBIM 準拠のモバイルブロードバンドインターフェイスを管理します。 認定デバイスが接続されている場合、追加のドライバーは必要なく、Windows はすぐにデバイスを使用してネットワークに接続できます。 モバイルブロードバンドクラスドライバーは、Windows mobile ブロードバンドドライバーモデルに準拠しており、Windows Mobile ブロードバンドサービスのすべての機能を提供します。 HSPA + および LTE を含む GSM ネットワークをサポートしています。CDMA ネットワーク;また、3G CDMA と 4G LTE を提供するデュアルモードネットワーク。 また、SMS、USSD、および EAP-SIM ベースの認証などのオペレーターメッセージもサポートしています。

**注**   モバイルブロードバンドクラスドライバーでは、USSD、EAP SIM、および複数の PDP コンテキストがサポートされていますが、デスクトップエディション (Home、Pro、Enterprise、および教育) のハードウェア認定要件では、windows 8、Windows 8.1、windows 10 のオプションのコンポーネントです。 ただし、ハードウェア認定を行うには、Windows 10 Mobile に複数の PDP コンテキストが必要です。

 

カスタムデバイスサービス拡張を使用して、追加のデバイス機能を実装できます。これは、WinRT デバイスサービス API を介してモバイルブロードバンドアプリに直接公開されます。

モバイルブロードバンドクラスドライバーの詳細については、「[モバイルブロードバンド (MB) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

### <a name="span-iddevice_service_extension_apispanspan-iddevice_service_extension_apispanspan-iddevice_service_extension_apispandevice-service-extension-api"></a><span id="Device_service_extension_API"></span><span id="device_service_extension_api"></span><span id="DEVICE_SERVICE_EXTENSION_API"></span>デバイスサービス拡張 API

Windows プラットフォームを使用する利点の1つは、オペレーターの区別をサポートする新しいハードウェアシナリオを提供できることです。 Windows mobile ブロードバンドプラットフォームでは、お客様のロイヤルティとブランドを高めることができるオペレーターを差別化することが期待されています。 プラットフォームには、独自のエクスペリエンスに組み込むことができる一連の拡張ポイントが用意されています。

Windows 認定のモバイルブロードバンドデバイスは、サポートされている各拡張ポイントを "デバイスサービス" として宣言します。 このようなサービスの例としては、電話帳、SIM Toolkit、GPS 機能などがあります。 Windows mobile ブロードバンドプラットフォームによってネイティブに実装されていないデバイスサービスには、デバイスサービス拡張 API を使用してアクセスできます。 ユーザーと IHV は、実装する必要があるデバイスサービスを定義します。 必要なデバイスサービスを有効にするには、IHV のファームウェアとモバイルブロードバンドアプリを同時に設計する必要があります。 USB 実装者フォーラムは、 [Mbimregistry](https://www.usb.org/)で ihv が利用できるデバイスサービスのレジストリを確立しています。また、このレジストリを使用して、一般的なデバイスサービス拡張の一貫性を確保することをお勧めします。

デバイスサービス拡張 API は、モバイルブロードバンドアプリがモバイルブロードバンドデバイスの機能にアクセスするための直接的な方法を提供します。 これにより、次の図に示すように、WWAN サービスとモバイルブロードバンドクラスドライバーを介してデバイスにパイプが提供されます。

![wwan サービスを介した情報フロー](images/mbae-hwguidelines-fig1.jpg)

各デバイスサービスには、対応する GUID があります。 モバイルブロードバンドクラスドライバーとデバイスとの間で交換されるすべてのコントロールメッセージと非 IP パケットは、その要求に関連付けられているサービスを識別するために GUID を使用します。 コマンド識別子 (Cid) と状態を示すコードは、サービスの GUID 名前空間で定義されています。 たとえば、電話帳と STK は同じ CID コードを共有できますが、要求で交換されるデバイスサービス GUID によって区別されます。

COM ベースのデバイスサービス API は、任意のデスクトップアプリケーションまたはサービスにアクセスできる   に**注意**してください。 WinRT プロジェクションデバイスサービス API は、モバイルブロードバンドオペレーターによって承認された privileged UWP デバイスアプリでのみ使用できます。 開発者は、この方法で情報をやり取りする際に、プライバシーとセキュリティを慎重に検討する必要があります。

 

Windows ワイヤレスプラットフォームは、アプリで使用できる次の機能用の Api をサポートしています。

-   デバイスサービスの列挙

-   デバイスサービスを開いて閉じる

-   特定のデバイスサービスへの制御コマンドの送信

-   特定のデバイスサービスとの間でデータを送受信する

-   特定のデバイスからの要請していないデバイスイベントに登録する

詳細については、「 [**Imbndeviceservice インターフェイス**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)」を参照してください。

### <a name="span-idlegacy_support_and_identity_morphingspanspan-idlegacy_support_and_identity_morphingspanspan-idlegacy_support_and_identity_morphingspanlegacy-support-and-identity-morphing"></a><span id="Legacy_support_and_identity_morphing"></span><span id="legacy_support_and_identity_morphing"></span><span id="LEGACY_SUPPORT_AND_IDENTITY_MORPHING"></span>レガシサポートと id のモーフィング

Windows 8、Windows 8.1、および Windows 10 は、Windows 7 向けに設計されたモバイルブロードバンドデバイスをサポートしています。 現在のデバイスのエコシステムは、windows 8、Windows 8.1、windows 10 でも引き続き機能しますが、windows 8、Windows 8.1、または Windows 10 mobile のブロードバンドプラットフォームを完全に利用することはできません。

Windows 8、Windows RT、Windows 8.1、Windows RT 8.1 でのモバイルブロードバンドデバイスのサポートの概要については、次を参照してください。

-   Windows 10 認定デバイス–これらのデバイスは、Windows 10 ハードウェア認定キットをサポートするモバイルブロードバンドエクスペリエンステストに合格します。 これらのデバイスの場合、Windows 10 はモバイルブロードバンドクラスドライバーと高度な電源管理機能を提供します。

-   Windows 8 または Windows 8.1 認定デバイス–これらのデバイスは、Windows 8 または Windows 8.1 ハードウェア認定キットをサポートするモバイルブロードバンドエクスペリエンステストに合格します。 これらのデバイスの場合、Windows 8 と Windows 8.1 は、モバイルブロードバンドクラスドライバーと高度な電源管理機能を提供します。

-   Windows 7 logo デバイス–これらのデバイスは、Windows 7 NDIS 6.20 ドライバーモデルに基づくサードパーティの IHV ドライバーを使用します。 Windows 8 と Windows 8.1 は、これらのデバイスの旧バージョンとの互換性モードでのモバイルブロードバンドエクスペリエンスを提供し、Windows 7 の機能に制限されています。

-   Windows 8 と Windows 8.1 は、以前のバージョンの Windows と同じように、モデムまたはイーサネットのインターフェイスとカスタム接続マネージャーを使用して、レガシデバイスのサポートを継続します。 Windows 8 と Windows 8.1 は、モバイルブロードバンドスタックに準拠していないため、モバイルブロードバンドエクスペリエンスを提供できません。 レガシデバイスはモバイルブロードバンドスタックで認識されないため、このようなデバイスを接続しても、Windows 接続マネージャーで管理されていないため、データの過剰消費が発生する可能性があります。

-   Windows RT および Windows RT 8.1 認定デバイス–これらのデバイスは、Windows RT または Windows RT 8.1 Windows ハードウェア認定キットでサポートされているモバイルブロードバンドエクスペリエンステストに合格します。 これらのデバイスの場合、Windows RT および Windows RT 8.1 は、モバイルブロードバンドクラスドライバーと高度な電源管理機能を提供します。

    Windows RT および Windows RT 8.1 システムでは、windows 7 以前のバージョン向けに設計されたモバイルブロードバンドデバイスはサポートされていませ**ん  。**

     

Windows 8 と Windows 8.1 認定デバイスが古いプラットフォームでも役立つように、Windows には id のモーフィングソリューションが用意されています。これにより、デバイスが接続されているオペレーティングシステムに適した動作をデバイスで表示できるようになります。

### <a name="span-ididentity_morphingspanspan-ididentity_morphingspanspan-ididentity_morphingspanidentity-morphing"></a><span id="Identity_morphing"></span><span id="identity_morphing"></span><span id="IDENTITY_MORPHING"></span>Id のモーフィング

デバイスが初めて Windows 7 PC に接続されている場合、一般的な外部モバイルブロードバンド USB ドングルは、大容量記憶装置として表示されます。 ドライバーソフトウェアが不足しているために、これらのデバイスが機能していないとして表示されないように、他の機能を公開することはありません。 大容量記憶装置には、ドライバーパッケージをインストールする IHV 提供のソフトウェアが含まれています。 ユーザーがドライバーパッケージをインストールした後、IHV 提供のソフトウェアは、他の機能をユーザーに公開するようにデバイスを変形させる必要があります。 この時点で、デバイスはモバイルブロードバンドデバイスとして表示され、ユーザーはネットワークに接続できます。

ネイティブ Windows 8、Windows 8.1、および Windows 10 クラスのドライバーを使用すると、ドライバーをインストールする必要がないため、外部 USB デバイスが最初に大容量記憶装置として公開される必要がなくなります。 Windows 8、Windows 8.1、Windows 10 には、デバイスの id のモーフィングをトリガーする機能が含まれています。これにより、デバイスはすぐにモバイルブロードバンドデバイスとして表示されるようになります。

Id のモーフィングソリューションを開発する方法については、 [**Imbndeviceservice インターフェイス**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)に関するページを参照してください。\]

### <a name="span-idfirmware_update_supportspanspan-idfirmware_update_supportspanspan-idfirmware_update_supportspanfirmware-update-support"></a><span id="Firmware_update_support"></span><span id="firmware_update_support"></span><span id="FIRMWARE_UPDATE_SUPPORT"></span>ファームウェアの更新のサポート

モバイルブロードバンドデバイスのファームウェアは、Windows Update を使用して更新する必要があります。 この方法の詳細については、「 [Windows 8 でのモバイルブロードバンドデバイスファームウェアの更新](https://docs.microsoft.com/windows-hardware/drivers/network/mobile-broadband-device-firmware-update)」を参照してください。 モバイルブロードバンドアプリを使用して、エクスペリエンスの特定の構成をプロビジョニングすることができます。

### <a name="span-idoma-dm_client_supportspanspan-idoma-dm_client_supportspanspan-idoma-dm_client_supportspanoma-dm-client-support"></a><span id="OMA-DM_client_support"></span><span id="oma-dm_client_support"></span><span id="OMA-DM_CLIENT_SUPPORT"></span>OMA-URI クライアントのサポート

BYOD (独自のデバイスを持ち込む) シナリオで Windows を実行しているデバイスを管理するために、企業向けの OMA-URI サポートを追加 Windows 8.1 ました。 これにより、サードパーティ製のモバイルデバイス管理プロバイダーと Windows InTune で使用するために、エンタープライズ関連のプロトコル ([.mde](https://go.microsoft.com/fwlink/?linkid=617595)、 [ms MDM](https://go.microsoft.com/fwlink/?linkid=619346)) を追加することで、これらのシナリオのサポートが拡張されます。

Windows は、モバイルネットワークオペレーター構成の OMA-URI サポートを enterprise BYOD のサポートから分離します。 Windows 8.1 と Windows 10 の OMA-URI クライアントは、モバイルオペレーター固有の設定をネイティブに構成することはできません。また、モバイルネットワークオペレーターの要件をサポートするためのサードパーティの拡張機能でもありません。 Windows Phone プラットフォームをサポートする OMA-URI ソリューションは、Windows 8.1 OMA-URI クライアントまたは Windows 10 OMA-URI クライアントと互換性がありません。

オペレーター固有の OMA-URI をサポートする場合は、次のオプションを検討してください。

-   OMA-URI クライアントがネットワークアダプターのファームウェアに存在する場合は、次のようになります。

    -   通常、モバイルブロードバンドデバイスの製造元は、オペレーター固有の OMA-URI クライアントをネットワークアダプターのファームウェアにバンドルすることができます。

    -   ネイティブでサポートされているソリューションが存在しない場合、モバイルブロードバンドデバイスの製造元は、ネットワークアダプターのファームウェアを統合するためのサードパーティの OMA-URI クライアントソリューションを提供できます。

    -   モバイルブロードバンドアプリでは、オペレーティングシステム固有のパラメーターを構成するときに、[プロビジョニングメタデータ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)を引き続き使用する必要があります。

-   モバイルブロードバンドアプリでの OMA-URI クライアント:

    -   モジュールがネットワークアダプターのファームウェアで OMA-URI クライアントをサポートしていない場合は、モバイルブロードバンドアプリに OMA-URI クライアントを実装することをお勧めします。

    -   このソリューションでは、モバイルブロードバンドアプリによってデバイス固有のパラメーターを構成するために、オペレーター固有またはデバイスの製造元固有のカスタムデバイスサービスがサポートされている必要があります。

    -   OMA-URI クライアントを含むモバイルブロードバンドアプリでは、オペレーティングシステム固有のパラメーターを構成するときに、[**プロビジョニングメタデータ**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)を使用する必要があります。

### <a name="span-idapn_managementspanspan-idapn_managementspanspan-idapn_managementspanapn-management"></a><span id="APN_Management"></span><span id="apn_management"></span><span id="APN_MANAGEMENT"></span>APN の管理

既定の APN 管理は、ローカル APN データベースを使用して行われます。 企業ユーザーなど、選択したユーザーの APN 情報を変更する必要がある場合があります。 このような場合は、OTA シグナリングで OMA-URI を使用して、デバイスで APN を直接更新することを選択できます。

デバイスには次のものが実装されている必要があります。

-   そのシステムの SIM を使用して接続が成功**する前に**、オペレーターが事前にプロビジョニングした場合、または OTA を通じてプロビジョニングした場合、デバイスは、mbim セクション10.5.13.5 で定義されているように Windows によって照会されると、Contexttype が**internet**に設定された最初のプロビジョニング済みコンテキストとしてインターネット PDP コンテキストを これにより、接続時に接続ロジックでこの APN 情報が使用されるようになります。

-   SIM を使用して、そのシステムの別の APN を使用してネットワークに正常に接続している場合は、ContextType をインターネットに設定しても機能しません。 新しい APN を使用して接続を確立するようにウィンドウを強制する唯一の方法は、作成された特定のプロファイルを削除することです。 このプロファイルを削除するには、管理者特権のコマンドプロンプトで**netsh mbn delete profile interface = "Mobile ブロードバンド Connection" name = "myProfileName"** というコマンドを実行します。

**注**   これはデバイスでサポートされるオプションの Windows 機能であるため、システム上でこのシナリオを検証するための HCK test や自動テストケースはありません。 オペレーターの認定では、デバイスがオペレーターの要件に準拠していることを確認するために検証を処理することを想定しています。

 

APN データベースの詳細については、「 [apn データベースの概要](apn-database-overview.md)」を参照してください。

### <a name="span-idnetwork_personalizationspanspan-idnetwork_personalizationspanspan-idnetwork_personalizationspannetwork-personalization"></a><span id="Network_personalization"></span><span id="network_personalization"></span><span id="NETWORK_PERSONALIZATION"></span>ネットワークの個人用設定

特定のオペレーターは、モバイルブロードバンド対応システムがネットワークにロックされているか、ロックされたデバイスのロックを解除してサービスの移植性を確保する必要があります。 このシナリオを有効にするには、Subsidy Lock の MBIM 仕様に含まれている\_種類のガイダンスで、OEM とデバイスのベンダーが MBIM\_PIN を使用する必要があります。

デバイスは、 [ **\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ready_info):: [**ReadyState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_ready_state)=**WwanReadyStateInitialized**をこのロック状態で\_報告する必要があり、 **WwanReadyStateDeviceLocked**を報告しないようにする必要があります。

デバイスに実装されているこの機能またはシステムが Windows で動作することを検証するための HCK テストケースがない   に**注意**してください。 OEM とオペレーターは、MBOT 内で特定のフィルターを使用して最終的な製品をテストできることを確認します。

 

 

 





