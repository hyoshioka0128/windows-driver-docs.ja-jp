---
title: SMS アプリの開発
description: SMS アプリの開発
ms.assetid: 052eb3cc-4a39-4667-8678-b18650f3b5c9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd269574dfc7fdf6e8f19d0fd0b3a033c9fcb3b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381474"
---
# <a name="developing-sms-apps"></a>SMS アプリの開発


Windows 8、Windows 8.1、および Windows 10 UWP アプリにモバイル ネットワーク オペレーター、モバイル ブロード バンド アダプター Ihv、Oem、および SMS のアクセス権を持つ、パートナーのソフトウェア ベンダーのアプリのショート メッセージ サービス (SMS) のテキスト メッセージング プラットフォームを提供します。

**注**  モバイル ブロード バンド アプリでは、テキスト メッセージを受信するときに、エンドユーザーに通知を表示する SMS のサポートが必要です。 SMS は規制要件や、特定の市場でのベスト プラクティスに準拠する必要もあります。

 

モバイル ブロード バンド SMS プラットフォームは、次の機能を提供します。

-   SMS テキスト モードまたは PDU モード (バイナリ) のデータの送受信

-   データの上限超過、移動、およびその他の管理用 SMS オペレーターの通知をフィルター処理します。

-   新しい SMS 受信したバック グラウンドのイベント

-   読み取りおよびモバイル ブロード バンド デバイス メッセージ ストアからのメッセージの削除

-   モバイル ブロード バンド デバイスのプロパティを取得します。

-   SMS API アクセスのプロンプト

このトピックのセクションでは、次のとおりです。

-   [モバイル ブロード バンド SMS がサポートされているデバイス](#supporteddevices)

-   [モバイル ブロード バンド SMS へのアクセス](#smsaccess)

-   [SMS 通知をフィルター処理](#filtering)

-   [SMS アプリの開発](#developsmsapp)

## <a name="span-idsupporteddevicesspanspan-idsupporteddevicesspanspan-idsupporteddevicesspanmobile-broadband-sms-supported-devices"></a><span id="SupportedDevices"></span><span id="supporteddevices"></span><span id="SUPPORTEDDEVICES"></span>モバイル ブロード バンド SMS がサポートされているデバイス


モバイル ブロード バンド接続で、SMS のしくみの概要図を示します。

![sms プラットフォームの概要](images/fig1-mb-sms-platformoverview.jpg)

### <a name="span-idbasreqspanspan-idbasreqspanbasic-requirements"></a><span id="basreq"></span><span id="BASREQ"></span>基本的な要件

-   コンピューターは、モバイル ネットワーク オペレーターから Windows 8、Windows 8.1、または Windows 10、モバイル ブロード バンド デバイス、およびアクティブなサービス、実行する必要があります。

-   デバイスは、SMS の送信/受信機能セットを Windows 8、Windows 8.1、または Windows 10 の認定されたハードウェアを配置する必要があります。

-   内部と外部の両方のデバイスがサポートされています。

-   Global System for Mobile Communications (GSM) - と Code division 複数 access (CDMA) - ベースのデバイスの両方がサポートされます。

### <a name="span-idadditionalguidanceforabetteruserexperiencespanspan-idadditionalguidanceforabetteruserexperiencespanspan-idadditionalguidanceforabetteruserexperiencespanadditional-guidance-for-a-better-user-experience"></a><span id="Additional_guidance_for_a_better_user_experience"></span><span id="additional_guidance_for_a_better_user_experience"></span><span id="ADDITIONAL_GUIDANCE_FOR_A_BETTER_USER_EXPERIENCE"></span>ユーザー エクスペリエンスを向上させるその他のガイダンス

-   SMS メッセージを送信またはデバイスがサポートされている演算子のネットワーク範囲の場合に、アプリで受信されたことができます。 デバイスは、ネットワーク サービス プロバイダーに登録する必要がありますが、メッセージを送受信するデータ サービスに接続する必要はありません。

-   送信または受信 SMS 中にネットワーク上のデータをローミングは、モバイル ネットワーク オペレーター (MNO) のポリシーに基づく追加料金が適用されます。

-   デバイスは、送信またはデバイスがロックされている PIN の場合は、SMS のデータを受信できません。

## <a name="span-idsmsaccessspanspan-idsmsaccessspanspan-idsmsaccessspanaccess-to-mobile-broadband-sms"></a><span id="SMSAccess"></span><span id="smsaccess"></span><span id="SMSACCESS"></span>モバイル ブロード バンド SMS へのアクセス


### <a name="span-idstorespanspan-idstorespanuwp-app-access-to-sms"></a><span id="store"></span><span id="STORE"></span>SMS への UWP アプリのアクセス

モバイル ブロード バンド SMS 機能にアクセスするには、次の方法があります。

-   モバイル ネットワーク オペレーターは、モバイル ブロード バンドのアプリを使用して、SMS の機能を持つユーザーを提供できます。

-   モバイル ブロード バンド アダプター Ihv オープン市場モバイル ブロード バンド アダプターを構築するには、SMS にアクセスする場合は、モバイル ブロード バンド アプリが有効にできます。

-   モバイル ブロード バンドのアダプターが埋め込まれているコンピューターを構築する Oem は、SMS にアクセスする場合は、モバイル ブロード バンド アプリを有効にできます。

-   UWP アプリを指定できる特権アクセス SMS 通信事業者、モバイル ブロード バンド アダプター IHV、または OEM によって。

SMS へのアクセスは、サービスのメタデータやデバイスのメタデータで指定されます。 デバイス メタデータ パッケージは、特定のデバイスとその UWP デバイスのアプリ間のリンクを作成する XML ファイルのセットです。 リンクは、モバイル ブロード バンドのアダプターが埋め込まれているコンピューターを構築する oem 向けの HardwareId の IHV モバイル ブロード バンド アダプター、またはコンピューターのハードウェア コンピューター デバイスのコンテナーの Id に基づいています。

サービス メタデータの詳細については、次を参照してください。[サービス メタデータ](service-metadata.md)します。

モバイル ネットワーク オペレーターと Ihv、Windows 8、Windows 8.1、および Windows 10 モバイル ブロード バンドのアダプターを自動的にダウンロードして、ユーザーが初めてデバイスを接続すると、Microsoft Store からモバイル ブロード バンドのアプリをインストールします。 Windows 8.1 および Windows 10 では、モバイル ブロード バンド アプリに追加されます、**すべてのアプリ**ビュー。

モバイル ブロード バンド アプリおよび IHV のアプリの 1 つのモバイル ブロード バンド デバイスの同時アクセス SMS があります。 モバイル ブロード バンド アプリと IHV および OEM の UWP アプリの両方がインストールされているし、新しい SMS を受信したときに、両方の表示通知のユーザー インターフェイス、ユーザーは通知の 2 つの Ui を参照してください。 ユーザーでは、通知をオフにしたり、アプリのいずれかをアンインストールすることができます。

### <a name="span-iduserspanspan-iduserspanuser-consent-to-sms-access"></a><span id="user"></span><span id="USER"></span>SMS へのアクセスをユーザーの同意

モバイル ブロード バンドのアプリでは、ユーザーのデバイスからのメッセージが原因で、携帯電話サービス プロバイダーからの送信または受信メッセージに対して課金されますユーザーを送信するために SMS を使用するユーザーの同意を取得する必要があります。

Windows 8 を実行しているユーザー、設定チャームを使用して、アプリ レベルの SMS 機能にアクセスを制御できるは、Windows 8.1、または Windows 10。

**注**  ユーザーの同意と、アプリも必要、デバイスまたはサービスのメタデータで、アプリ名を追加することで、デバイスによって付与されたアクセス。

 

## <a name="span-idfilteringspanspan-idfilteringspanspan-idfilteringspansms-notifications-filtering"></a><span id="Filtering"></span><span id="filtering"></span><span id="FILTERING"></span>SMS 通知をフィルター処理


モバイル ブロード バンド SMS プラットフォームは、2 種類に新しく受信した SMS のデータをフィルター処理: モバイル ネットワーク オペレーター (MNO) および一般的な SMS メッセージから SMS 通知を管理します。 MNO から受信した SMS 通知を管理はのみ、モバイル ブロード バンドのアプリにアクセスでき、一般的な SMS クライアント アプリは表示されません。

MNOs は、Windows のプロビジョニングし、プラットフォームに SMS 通知の管理用のカスタムのフィルタ リング規則を指定します。 メッセージのフィルタ リング規則が指定されていない場合、SMS プラットフォームはすべてのアプリに使用できる一般的な SMS メッセージとしてすべての SMS メッセージを分類します。

通知フィルターの詳細については、次を参照してください。 [mobile operator notifications とシステム イベントを有効にする](enabling-mobile-operator-notifications-and-system-events.md)します。

## <a name="span-iddevelopsmsappspanspan-iddevelopsmsappspanspan-iddevelopsmsappspandeveloping-your-sms-app"></a><span id="DevelopSMSApp"></span><span id="developsmsapp"></span><span id="DEVELOPSMSAPP"></span>SMS アプリの開発


JavaScript を記述するC#、またはを使用する C++ アプリ、 [ **Windows.Devices.Sms** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Sms)送信、読み取り、およびメッセージを削除する API。

**注**   Windows 7 モバイル ブロード バンド SMS API は、SMS のモデムの低レベル インターフェイスのみを提供します。 Windows 8、Windows 8.1、および Windows 10 は、全般的なアプリ開発に適した代替のテキスト モード インターフェイスを提供します。

 

-   [SMS デバイス ストレージの制限](sms-device-storage-limits.md)

-   [SMS のデバイスを列挙します。](enumerate-sms-devices.md)

-   [SMS デバイス情報を取得します。](get-sms-device-information.md)

-   [読み取りがテキスト モード インターフェイスを使用して SMS を受信しました](read-received-sms-by-using-the-text-mode-interface.md)

-   [新しい受信 SMS のバック グラウンド イベントを実行します。](run-new-sms-received-background-events.md)

-   [カスタム文字セットを使用して SMS を送信します。](send-sms-by-using-custom-character-sets.md)

-   [テキスト モード インターフェイスを使用して SMS を送信します。](send-sms-by-using-the-text-mode-interface.md)

-   [SMS 宣言のセット](set-sms-declarations.md)

 

 





