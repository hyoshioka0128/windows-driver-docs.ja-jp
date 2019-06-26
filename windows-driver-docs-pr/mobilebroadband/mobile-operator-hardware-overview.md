---
title: 通信事業者のハードウェアの概要
description: 通信事業者のハードウェアの概要
ms.assetid: b2322972-16be-443f-b46a-7834b4d7ead0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4214393f781662e11d8ace8fdb07567be94fd9e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393422"
---
# <a name="mobile-operator-hardware-overview"></a>通信事業者のハードウェアの概要


このトピックを使用して、Windows 8、Windows 8.1、および Windows 10 モバイル ブロード バンド ハードウェア要件および推奨事項の概要を理解する必要があります。 簡略化された接続を使用して顧客のエクスペリエンスに加え、メンテナンスの削減とサポートのコストを提供するには、次をお勧めします。

-   USB インターフェイスを提供する埋め込みのモバイル ブロード バンドのモジュールは、Windows 8、Windows 8.1、または Windows 10 のハードウェア認定要件を満たす必要があり、モバイル ブロード バンド クラス ドライバーを使用して管理します。 Ihv 向けのハードウェアの要件に関するドキュメントは、モバイル ブロード バンド デバイスが Windows 8、Windows 8.1、または Windows 10 デバイスの証明に合格する必要があります。

-   外部 USB モバイル ブロード バンド ドングルでは、id モーフィングをサポートする必要があります。 Ihv 向けのハードウェアの要件に関するドキュメントは、外部のモバイル ブロード バンド デバイスが Windows 8 デバイスの認定、Windows 8.1、または Windows 10 デバイスの証明書の両方を渡すし、Windows 7 のロゴ認定を渡す必要があります。

    -   Windows 10 コンピューターでは、ドングルはモバイル ブロード バンド デバイスの認定、Windows 10 として表示され、モバイル ブロード バンド クラス ドライバーを使用して管理されます。

    -   Windows 8.1 コンピューターでは、ドングルは、Windows 8.1 モバイル ブロード バンド デバイスを認定として表示され、モバイル ブロード バンド クラス ドライバーを使用して管理されます。

    -   Windows 8 コンピューターでは、ドングルは、Windows 8 モバイル ブロード バンド デバイスを認定として表示され、モバイル ブロード バンド クラス ドライバーを使用して管理されます。

    -   Windows 7 コンピューターで、ユーザーが特定のデバイス ドライバーをインストールできるように、大容量記憶装置としてドングルが表示されます。

-   EAP-SIM、USSD、または複数の PDP 接続が必要な場合は、IHV が有効にする必要があり、Windows 8、Windows 8.1、または Windows 10 のハードウェア認定要件を遵守する必要があります。

-   デバイス サービス拡張機能を使用して、モバイル ブロード バンド クラス ドライバーとデバイスのサービス Api を使用して Windows 8、Windows 8.1、または Windows 10 で有効にするか、IHV によって必要な機能の追加を実装しなければなりません。 ハードウェア要件のドキュメントの一部として他の機能を含める必要があります。

## <a name="span-idkeyscenariosspanspan-idkeyscenariosspanspan-idkeyscenariosspankey-scenarios"></a><span id="Key_scenarios"></span><span id="key_scenarios"></span><span id="KEY_SCENARIOS"></span>主なシナリオ


### <a name="span-idpurchaseanexternaldevicespanspan-idpurchaseanexternaldevicespanspan-idpurchaseanexternaldevicespanpurchase-an-external-device"></a><span id="Purchase_an_external_device"></span><span id="purchase_an_external_device"></span><span id="PURCHASE_AN_EXTERNAL_DEVICE"></span>外部デバイスを購入します。

外部デバイス、ユーザーが使用を開始する前にすぐに挿入される可能性があります。

1.  デバイスが挿入されるとすぐに認識され、モバイル ブロード バンド クラス ドライバーによって管理されます。

2.  モバイル ブロード バンド サービスでは、IMSI を読み取ってハッシュ セットを生成します。

3.  ユーザーがクリックしたとき**Connect**、これらのハッシュが内の接続の設定に一致するように使用される、 [COSA/APN データベースの送信](cosa-apn-database-submission.md)。

    -   接続が成功すると、インターネット接続が利用できる場合は、さらに何も起こりません。 ユーザーがサービスを既に購入します。

    -   接続が成功すると、インターネット接続が利用できない場合は、APN データベースまたはモバイル ブロード バンド UWP アプリで指定された URL に web ブラウザーを開きます。

    -   接続に失敗した場合、ユーザーは、エラーの通知します。

4.  Web サイトまたはモバイル ブロード バンド アプリ サービスを購入するユーザーに役立ちます。

5.  、購入後、デバイスはプロビジョニング ファイルからプロビジョニング API を使用してプロビジョニングされます。 プロビジョニング ファイルは、web サイトまたはモバイル ブロード バンド アプリでプロビジョニング エージェントに渡されます。 プロビジョニング ファイルは、ユーザーが購入したプランに関する基本情報を Windows を構成します。 ネットワークの構造によっては、次のいずれかが発生します。

    -   現在の接続でインターネット アクセスをユーザーに許可します。

    -   プロビジョニング ファイルには、切断し、同じネットワークまたはインターネットへのアクセスを提供する別のネットワークに再接続する手順が含まれています。

### <a name="span-idconnectanexternaldevicewithanactivesimspanspan-idconnectanexternaldevicewithanactivesimspanspan-idconnectanexternaldevicewithanactivesimspanconnect-an-external-device-with-an-active-sim"></a><span id="Connect_an_external_device_with_an_active_SIM"></span><span id="connect_an_external_device_with_an_active_sim"></span><span id="CONNECT_AN_EXTERNAL_DEVICE_WITH_AN_ACTIVE_SIM"></span>アクティブな SIM で外部のデバイスを接続します。

アクティブなデバイスがアクティブの SIM が既にアタッチされている、インターネットに接続試行につながることを除いて、ワークフローには外部のデバイスを購入した場合に似ています。 サービスを購入する web サイトやモバイル ブロード バンドのアプリをユーザーに指示する必要はありません。

1.  デバイスが挿入されるとすぐに認識され、モバイル ブロード バンド クラス ドライバーによって管理されます。

2.  モバイル ブロード バンド サービスでは、IMSI を読み取ってハッシュ セットを生成します。

3.  ユーザーがクリックしたとき**Connect**、これらのハッシュが内の接続の設定に一致するように使用される、 [COSA/APN データベースの送信](cosa-apn-database-submission.md)。 アクティブな SIM でデバイスの場合、接続が成功したとインターネット接続が使用可能です。

## <a name="span-idcomponentsspanspan-idcomponentsspanspan-idcomponentsspancomponents"></a><span id="Components"></span><span id="components"></span><span id="COMPONENTS"></span>コンポーネント


### <a name="span-idwindows8windows81orwindows10certifiedmobilebroadbanddevicesspanspan-idwindows8windows81orwindows10certifiedmobilebroadbanddevicesspanspan-idwindows8windows81orwindows10certifiedmobilebroadbanddevicesspanwindows8-windows81-or-windows10-certified-mobile-broadband-devices"></a><span id="Windows_8__Windows_8.1__or_Windows_10_certified_mobile_broadband_devices"></span><span id="windows_8__windows_8.1__or_windows_10_certified_mobile_broadband_devices"></span><span id="WINDOWS_8__WINDOWS_8.1__OR_WINDOWS_10_CERTIFIED_MOBILE_BROADBAND_DEVICES"></span>Windows 8、Windows 8.1、または Windows 10 モバイル ブロード バンド デバイスを認定

Windows モバイル ブロード バンド プラットフォームを最大限に活用するには、モバイル ブロード バンド デバイスは、Windows 8、Windows 8.1、または Windows 10 のハードウェア認定要件を満たす必要があります。 ハードウェア認定の要件の包括的な説明は、次を参照してください。 [Windows ハードウェア認定要件](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/)します。

エンドユーザーの最も単純な接続エクスペリエンスは USB ベースのモバイル ブロード バンド デバイスに配信されます。 ハードウェア認定の要件の一部として、USB デバイスとしてマニフェストのすべてのモバイル ブロード バンド デバイスが準拠する必要があります、[モバイル ブロード バンド インターフェイス モデル (MBIM) 仕様](https://docs.microsoft.com/windows-hardware/drivers/network/mb-interface-model)MBIM v1.0 の正誤表とします。 これには、外部 USB ドングルと USB インターフェイスを提供する組み込みのモジュールの両方が含まれます。 このクラス デバイスでは、には Windows 8、Windows 8.1、または Windows 10 には、IHV から追加のドライバーが不要し、ユーザーの接続エクスペリエンスを簡略化モバイル ブロード バンド クラス ドライバーが含まれます。 USB ドライバー モデルではないその他のハードウェアが Windows 8、Windows 8.1、および Windows 10 の証明書を受信できるし、Microsoft Store モバイル ブロード バンド アプリ エクスペリエンスを提供しますが、モバイル ブロード バンド クラス ドライバーではサポートされていません。

### <a name="span-idmobilebroadbandclassdriverspanspan-idmobilebroadbandclassdriverspanspan-idmobilebroadbandclassdriverspanmobile-broadband-class-driver"></a><span id="Mobile_broadband_class_driver"></span><span id="mobile_broadband_class_driver"></span><span id="MOBILE_BROADBAND_CLASS_DRIVER"></span>モバイル ブロード バンド クラス ドライバー

モバイル ブロード バンド クラス ドライバーは、その特定のモバイル ブロード バンド デバイス用のカスタム ドライバーを提供するデバイスの製造元の負担を軽減できです。 モバイル ブロード バンド クラス ドライバーは、すべて USB MBIM 準拠しているモバイル ブロード バンド インターフェイスを満たす Windows 8、Windows 8.1、または Windows 10 デバイスの証明書を管理します。 認定されたデバイスが接続されると、ドライバーを追加する必要がないと、ネットワークに接続するデバイスをすぐに使用できる Windows。 モバイル ブロード バンド クラス ドライバーは、Windows のモバイル ブロード バンド ドライバー モデルに準拠しているし、Windows モバイル ブロード バンド サービスへの完全な機能を提供します。 GSM ネットワーク、HSPA +、LTE; などをサポートしていますCDMA ネットワークデュアル モードのネットワーク サービスの 3 G CDMA と 4 G LTE います。 また、SMS、USSD、EAP SIM ベースの認証などの演算子のメッセージもサポートしています。

**注**   USSD、EAP-SIM、および複数の PDP コンテキストがモバイル ブロード バンド クラス ドライバーによってサポートされている、Windows 8、Windows 8.1、または Windows 10 のデスクトップ エディションの場合の省略可能なコンポーネント (Home、Pro、Enterprise、および教育機関向け) ハードウェア認定要件。 複数の PDP コンテキストがただしハードウェア認定、Windows 10 Mobile に必要です。

 

WinRT デバイスのサービス API を使用してモバイル ブロード バンド アプリに直接公開されるカスタムのデバイス サービス拡張機能を使用して、追加のデバイスの機能を実装できます。

モバイル ブロード バンド クラス ドライバーの詳細については、次を参照してください。[モバイル ブロード バンド (MB) の参照を](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

### <a name="span-iddeviceserviceextensionapispanspan-iddeviceserviceextensionapispanspan-iddeviceserviceextensionapispandevice-service-extension-api"></a><span id="Device_service_extension_API"></span><span id="device_service_extension_api"></span><span id="DEVICE_SERVICE_EXTENSION_API"></span>デバイス サービス拡張機能 API

Windows プラットフォームを使用する個別の利点の 1 つは、演算子の差別化をサポートするハードウェアの新しいシナリオを提供する機能です。 Windows モバイル ブロード バンド プラットフォームは、上位の顧客ロイヤルティをブランド価値に頼れるコマンドできます演算子を差別化を有効にすると想定されます。 プラットフォームは、一意のエクスペリエンスに組み込むことができます拡張点のセットを提供します。

Windows では、モバイル ブロード バンド デバイス"device service"としてサポートされている拡張機能の各点の宣言が認定されています。 このようなサービスの例には、電話帳、SIM Toolkit または GPS 機能が含まれます。 Windows モバイル ブロード バンド プラットフォームでネイティブに実装されていないすべてのデバイス サービスは、デバイス サービス拡張機能 API を使用してアクセスできます。 IHV は、実装する必要があるデバイスのサービスを定義します。 IHV のファームウェアとモバイル ブロード バンド アプリは、目的のデバイスのサービスを有効に同時に設計する必要があります。 Ihv で使用できるデバイスのサービスのレジストリの確立は、USB Implementers Forum [MBIMRegistry](https://www.usb.org/)とするおよび使用している Ihv が一貫性を保つために調整するこのレジストリを使用していることをお勧めします。一般的なデバイス サービス拡張機能。

デバイス サービス拡張機能 API では、モバイル ブロード バンド デバイス機能にアクセスする場合は、モバイル ブロード バンド アプリの直接的な方法を提供します。 次の図に示すようにこれ WWAN サービスと、デバイスにモバイル ブロード バンド クラス ドライバーのコンジットを提供します。

![wwan サービスを介して、情報の流れ](images/mbae-hwguidelines-fig1.jpg)

各デバイスのサービスでは、対応する GUID があります。 すべてのコントロール メッセージと、モバイル ブロード バンド クラス ドライバーとデバイス間で交換される非 IP パケットは、要求に関連付けられたサービスを識別する GUID を実行します。 コマンド識別子 (Cid) と状態を示す値のコードは、サービスの GUID の名前空間で定義されます。 たとえば、電話帳と STK 同じ CID コードでは、両方を共有する可能性がありますが、要求の GUID が交換される、デバイス サービスによって識別されます。

**注**   COM ベースのデバイス サービス API は、デスクトップ アプリケーションまたはサービスにアクセスできます。 射影されたデバイスのサービス API はモバイル ブロード バンド演算子によって権限を持つ特権のある UWP デバイス アプリにのみ使用可能な WinRT します。 開発者を十分に検討のプライバシーとセキュリティ情報をこのように通信するときにします。

 

Windows のワイヤレス プラットフォームには、アプリで使用できるは、次の機能の Api がサポートされています。

-   デバイスのサービスを列挙します。

-   Open および close デバイス サービス

-   特定のデバイス サービスに管理コマンドを送信します。

-   送信または受信する、または特定のデバイス サービスからのデータ

-   特定のデバイスからイベントを要請していないデバイスの登録します。

詳細については、次を参照してください。 [ **IMbnDeviceService インターフェイス**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)します。

### <a name="span-idlegacysupportandidentitymorphingspanspan-idlegacysupportandidentitymorphingspanspan-idlegacysupportandidentitymorphingspanlegacy-support-and-identity-morphing"></a><span id="Legacy_support_and_identity_morphing"></span><span id="legacy_support_and_identity_morphing"></span><span id="LEGACY_SUPPORT_AND_IDENTITY_MORPHING"></span>レガシ サポートし、id モーフィング

Windows 8、Windows 8.1、および Windows 10、Windows 7 用に設計された、モバイル ブロード バンド デバイスをサポートします。 デバイスの現在のエコシステムは引き続き Windows 8、Windows 8.1、および Windows 10 の機能がフルに活用 Windows 8、Windows 8.1、または Windows 10 モバイル ブロード バンド プラットフォーム。

モバイル ブロード バンド デバイス サポート inWindows 8、Windows RT、Windows 8.1、および Windows RT 8.1 の概要を次に示します。

-   Windows 10 デバイスを認定する – これらのデバイスが Windows 10 のハードウェア認定キットをサポートしているモバイル ブロード バンド エクスペリエンスのテストに合格します。 これらのデバイスで Windows 10 には、モバイル ブロード バンド クラス ドライバーおよび電源管理の詳細。

-   Windows 8 または Windows 8.1 認定デバイス – これらのデバイスが Windows 8 または Windows 8.1 のハードウェア認定キットをサポートしているモバイル ブロード バンド エクスペリエンスのテストに合格します。 これらのデバイスで Windows 8 および Windows 8.1 でモバイル ブロード バンド クラス ドライバーが提供し、電源管理の詳細。

-   Windows 7 ロゴは、デバイスを取得した – これらのデバイスが Windows 7 6.20 が動作 NDIS ドライバー モデルに基づいて、サードパーティ IHV ドライバーを使用します。 Windows 8 および Windows 8.1 は、これらのデバイスの下位互換性モードでのモバイル ブロード バンド エクスペリエンスを提供し、Windows 7 の機能に制限されています。

-   Windows 8 および Windows 8.1 のモデムまたはイーサネット インターフェイスを Windows の以前のバージョンと同様に、カスタム接続マネージャーと共にに基づく従来のデバイスのサポートを継続します。 Windows 8 および Windows 8.1 はモバイル ブロード バンド モバイル ブロード バンド スタックに準拠していないのでのエクスペリエンスを提供できません。 従来のデバイスがモバイル ブロード バンド スタックによって認識されないため、このようなデバイス経由で接続が原因で過度なデータ使用ように Windows 接続マネージャーで、管理されていません。

-   Windows RT と Windows RT 8.1 認定デバイス – これらのデバイスが Windows RT または Windows RT 8.1 Windows ハードウェア認定キットでサポートされているモバイル ブロード バンド エクスペリエンスのテストに合格します。 これらのデバイスで Windows RT と Windows RT 8.1 でモバイル ブロード バンド クラス ドライバーが提供し、電源管理の詳細。

    **注**   Windows RT と Windows RT 8.1 のシステムでは、Windows 7 と以前のバージョン用に設計された、モバイル ブロード バンド デバイスをサポートしていません。

     

Windows 8 および Windows 8.1 の認定デバイスが古いプラットフォーム上に有用であることを確認は、Windows は、id モーフィング、デバイスが接続されているオペレーティング システムの適切な動作を実現するソリューションを提供します。

### <a name="span-ididentitymorphingspanspan-ididentitymorphingspanspan-ididentitymorphingspanidentity-morphing"></a><span id="Identity_morphing"></span><span id="identity_morphing"></span><span id="IDENTITY_MORPHING"></span>Id モーフィング

デバイスは Windows 7 PC に初めて接続された、一般的な外部モバイル ブロード バンド USB ドングルは自体の大容量記憶装置としてに表示されます。 これには、これらのデバイスとして非機能的なドライバー ソフトウェアがないため表示されないようにするには、その他の機能は公開されません。 大容量記憶装置には、ドライバー パッケージをインストールする IHV が指定したソフトウェアが含まれています。 ユーザーがドライバー パッケージをインストールした後、IHV が指定したソフトウェアはユーザーにその他の関数を公開するデバイスを変形する必要があります。 この時点では、デバイスがモバイル ブロード バンド デバイスとして表示され、ユーザーがネットワークに接続できます。

ネイティブの Windows 8、Windows 8.1、および Windows 10 のクラス ドライバーをドライバーのインストールは必要ありませんので、大容量記憶装置のデバイスとして最初に公開自体の外部の USB デバイスの必要はありません。 Windows 8、Windows 8.1、および Windows 10 デバイスの id モーフィング、すぐにモバイル ブロード バンド デバイスとして表示するデバイスをトリガーする機能が含まれます。

Id モーフィング ソリューションを開発する方法については、次を参照してください。 [ **IMbnDeviceService インターフェイス**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbndeviceservice)します。\]

### <a name="span-idfirmwareupdatesupportspanspan-idfirmwareupdatesupportspanspan-idfirmwareupdatesupportspanfirmware-update-support"></a><span id="Firmware_update_support"></span><span id="firmware_update_support"></span><span id="FIRMWARE_UPDATE_SUPPORT"></span>ファームウェア更新プログラムのサポート

Windows Update を使用して、モバイル ブロード バンド デバイス ファームウェアを更新する必要があります。 これを実行する方法については、次を参照してください。[モバイル ブロード バンド デバイス ファームウェアの更新を Windows 8 で](https://docs.microsoft.com/windows-hardware/drivers/network/mobile-broadband-device-firmware-update)します。 お客様のエクスペリエンスに固有の構成は、モバイル ブロード バンド アプリを使用してプロビジョニングできます。

### <a name="span-idoma-dmclientsupportspanspan-idoma-dmclientsupportspanspan-idoma-dmclientsupportspanoma-dm-client-support"></a><span id="OMA-DM_client_support"></span><span id="oma-dm_client_support"></span><span id="OMA-DM_CLIENT_SUPPORT"></span>OMA DM クライアントのサポート

Windows 8.1 では、BYOD (Bring Your Own Device) シナリオで Windows を実行しているデバイスを管理する企業向けの OMA-DM サポートが追加されました。 ここでエンタープライズ関連プロトコルを追加することでこれらのシナリオのサポートを拡張 ([MS MDE](https://go.microsoft.com/fwlink/?linkid=617595)、 [MS MDM](https://go.microsoft.com/fwlink/?linkid=619346)) サード パーティのモバイル デバイス管理のプロバイダーと Windows InTune で使用します。

Windows では、enterprise が BYOD のサポートからのモバイルのネットワーク オペレーター構成の OMA-DM サポートを分離します。 Windows 8.1 および Windows 10 の OMA DM クライアントがモバイル演算子固有設定の構成をサポートしていないネイティブとはないサード パーティの拡張可能なモバイルをサポートするネットワーク オペレーター要件。 Windows Phone プラットフォームをサポートする、OMA-DM ソリューションは、Windows 8.1 の OMA-DM クライアントまたは Windows 10、OMA-DM クライアントと互換性がないです。

オペレーターの特定 OMA-DM をサポートするときに考慮すべきいくつかのオプションを次に示します。

-   OMA DM クライアントのネットワーク アダプターのファームウェアの場合。

    -   通常、モバイル ブロード バンド デバイスの製造元は、そのネットワーク アダプターのファームウェアでオペレーターの特定の OMA DM クライアントをバンドルする可能性があります。

    -   モバイル ブロード バンド デバイスの製造元は、ネイティブにサポートされているソリューションが存在しない場合、そのネットワーク アダプターのファームウェアで統合するためのサード パーティ製の OMA DM クライアント ソリューションを提供することができます。

    -   モバイル ブロード バンドのアプリを引き続き使用する必要があります[プロビジョニング メタデータ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)オペレーティング システム固有のパラメーターを構成するときにします。

-   モバイル ブロード バンド アプリでの OMA DM クライアント:

    -   モジュールは、ネットワーク アダプターのファームウェアでを OMA DM クライアントをサポートする場合、モバイル ブロード バンド アプリで OMA DM クライアントを実装することがあります。

    -   このソリューションでは、モバイル ブロード バンド アプリによってデバイス固有のパラメーターを構成するために固有の演算子またはデバイスの製造元に固有のカスタム デバイス サービス サポートが必要です。

    -   モバイル ブロード バンド アプリを含む、OMA DM クライアントを使用する必要があります[**プロビジョニング メタデータ**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)オペレーティング システム固有のパラメーターを構成するときにします。

### <a name="span-idapnmanagementspanspan-idapnmanagementspanspan-idapnmanagementspanapn-management"></a><span id="APN_Management"></span><span id="apn_management"></span><span id="APN_MANAGEMENT"></span>APN の管理

既定の APN 管理は、ローカルの APN database を使用して行われます。 APN 情報が、エンタープライズ ユーザーなど、選択的なユーザーの変更が必要な場合があります。 このような場合、または OEM は、OTA 信号で OMA-DM を使用してデバイス上で直接、APN を更新する選択できます。

デバイスを次に実装する必要があります。

-   演算子による事前プロビジョニング、ota プロビジョニングまたは**より前のバージョン**SIM を使用して、そのシステム上で、接続に成功、デバイスがようにインターネット PDP コンテキスト、ContextType を最初にプロビジョニングされたコンテキストに設定**インターネット**MBIM 10.5.13.5 セクションで定義されている Windows が照会するとします。 これにより、接続ロジックが、接続時に、この APN 情報を使用します。

-   SIM は、そのシステム上で別の APN を使用してネットワークに成功した接続を確立するために使われている、ContextType をインターネットに設定は機能しません。 ウィンドウが強制的に新しい APN を使用して接続を確立する唯一の方法では、作成した特定のプロファイルを削除します。 管理者特権でコマンド プロンプトから次のコマンドを実行して、プロファイルを削除できます: **netsh mbn プロファイル インターフェイスの削除「モバイル ブロード バンド接続」名前 ="myProfileName"を =**

**注**   HCK テストまたはシステムでは、このシナリオを検証する自動テスト_ケースがないこれは、デバイスをサポートするためのオプションの Windows 機能であるためです。 演算子証明書が、デバイスが演算子の要件に準拠していることを確認する検証を処理することを予想することをお勧めします。

 

APN データベースに関する詳細については、次を参照してください。 [APN データベースの概要](apn-database-overview.md)します。

### <a name="span-idnetworkpersonalizationspanspan-idnetworkpersonalizationspanspan-idnetworkpersonalizationspannetwork-personalization"></a><span id="Network_personalization"></span><span id="network_personalization"></span><span id="NETWORK_PERSONALIZATION"></span>ネットワークのパーソナル化

特定の演算子は、モバイル ブロード バンド対応のシステムは、そのネットワークにロックする必要がありますまたはサービスの移植性のためにロックされているデバイスのロックを解除する要件があります。 このシナリオを有効にする OEM のですがとデバイスのベンダーを使用して、MBIM\_PIN\_Subsidy ロック MBIM 仕様の型のガイダンス。

デバイスを報告する必要があります[ **WWAN\_準備\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ready_info):。[**ReadyState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ne-wwan-_wwan_ready_state)=**WwanReadyStateInitialized**このロックの状態とを報告しない**WwanReadyStateDeviceLocked**します。

**注**  デバイスでこの機能が実装されているかを検証する HCK テスト ケースがないか、システムは Windows で動作します。 MBOT 内の特定のフィルターを使用して最終製品をテストできることを確認するには、OEM と演算子に注目します。

 

 

 





