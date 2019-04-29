---
title: アカウントのプロビジョニング
description: アカウントのプロビジョニング
ms.assetid: 3ffcd769-253f-4918-8095-a9206445a201
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbf7dc1f67600a9deccc4773d733330654744c7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386916"
---
# <a name="account-provisioning"></a>アカウントのプロビジョニング

プロビジョニングは、オペレーターのネットワークに接続するために必要な情報を Windows コンピューターの構成を表します。 通常、プロビジョニングは、モバイル ブロード バンドのサブスクリプションの購入後に実行します。 Windows では、演算子から XML ベースのプロビジョニング ファイルを受け入れます。 プロビジョニング API では、モバイル ブロード バンドのアプリを使用するか、購入の web サイトに、演算子からプロビジョニング XML ファイルを適用します。

次の図は、コンテンツおよびプロビジョニング XML ファイルの階層を示します。

![xml ファイルの階層のプロビジョニング](images/mb-provisioningmetadata.jpg)

プロビジョニングのスキーマの詳細については、次を参照してください。 [CarrierControlSchema スキーマ](https://msdn.microsoft.com/library/windows/apps/hh868312)します。

## <a name="updating-the-provisioning-metadata"></a>プロビジョニングのメタデータを更新します。

コンピューターのプロビジョニングのメタデータを更新するいくつかの方法はあります。

### <a name="mobile-broadband-app"></a>モバイル ブロード バンド アプリ

モバイル ブロード バンド アプリは、コンピューターにインストールした後、取得または更新されたアプリに実装する任意のトリガーに基づくプロビジョニング ファイルを生成することできます。

モバイル ブロード バンド アプリを使用してプロビジョニング ファイルを適用することができます、 [ **Windows.Networking.NetworkOperator.ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397) Api。 使用できる場合は、アプリは、ネットワーク アカウントの ID に関連付けられて、 [ **CreateFromNetworkAccountId** ](https://msdn.microsoft.com/library/windows/apps/br207398)符号なしのメタデータを提供します。 既定のコンス トラクターを使用する必要があります、アプリが、ネットワーク アカウント ID と関連付けられていない場合は、 **ProvisioningAgent**し、XML に署名します。

モバイル ブロード バンド アプリは、次のトリガーを使用して、プロビジョニングのメタデータを更新できます。

- **使用状況**後、データの制限は最初に構成すると、すべて 5% の使用状況の増分でアプリに通知を Windows がわかります。 これにより、アプリが最新の使用状況情報を取得します。

- **タイマー**タイマーは、適切な時間間隔でプロビジョニングのメタデータを更新できます。

- **受信した SMS**アプリで認識される SMS メッセージを送信することができます。 これには、更新を開始します。 または、しきい値通知を受信すると、更新された使用量を自動的にチェックするメッセージを定義します。

- **Windows 通知サービス**Any UWP アプリがプッシュ通知を登録し、コンテンツに基づいてアクションを実行します。 この操作は、更新プログラムをプロビジョニングするため、通知チャンネルとして使用できます。

- **大規模な場所の変更**場所の変更がユーザーの新しい場所に更新された設定を適用するアプリをトリガー可能性がありますさまざまなパラメーターは、さまざまなロケールであるユーザーに適用される場合。

- **タイム ゾーンの変更**大きな領域サイズは、システムのタイム ゾーンの変更として使用できます、プロキシの場所を変更します。 これは、GPS またはモバイル ブロード バンドを持たないコンピューターで興味のあることができます。

### <a name="web-based-provisioning"></a>Web ベースのプロビジョニング

Web サイトを使用してプロビジョニング データを指定できます、 [ **window.external.msProvisionNetworks** ](https://msdn.microsoft.com/library/hh848316) API。 この API に渡されるファイルのプロビジョニングは、X.509 証明書と XML DSig を使用して署名する必要があります。

証明書は、APN データベース、サービスのメタデータまたはメタデータ ファイルをプロビジョニングする前のアカウントを使用して、コンピューターを事前に用意されたであることができます。 証明書は既に信頼されている場合、ユーザー操作はありません。 証明書は、コンピューターにまだは認識されて、EV 証明書である必要があり、証明書を受け入れる前に同意を求められます。

### <a name="automatic-provisioning-refresh"></a>自動プロビジョニングの更新

プロビジョニング ファイルには、特定の SMS メッセージに応答したり、スケジュールされた間隔で更新されたプロビジョニング ファイルを自動的に取得する Windows のためのディレクティブを含めることができます。 このメソッドでは、モバイル ブロード バンド アプリがローカル コンピューターにインストールすることは必要ありません。

## <a name="provisioning-metadata-contents"></a>プロビジョニングのメタデータの内容

プロビジョニングのメタデータには、次のセクションが含まれています。

- [グローバル](#global)

- [アクティブ化](#activation)

- [モバイル ブロード バンド情報](#mobile-broadband-information)

- [Wi-fi 情報](#wi-fi-information)

- [プラン情報](#plan-information)

- [[更新]](#refresh)

- [署名](#signature)

- [許可されている組み合わせ](#permitted-combinations)

これらのセクションの詳細については、次を参照してください。 [CarrierControlSchema スキーマ](https://msdn.microsoft.com/library/windows/apps/hh868312)します。

### <a name="global"></a>グローバル

グローバル セクションは、プロビジョニングのすべてのファイルに必要です。 このセクションで必要な要素は次のとおりです。

- [**CarrierId** ](https://msdn.microsoft.com/library/windows/apps/hh868288)ファイルを作成した組織を一意に識別する GUID。 モバイル ブロード バンドのアプリを構築する場合で指定した GUID を使用する必要があります、[サービス数](https://msdn.microsoft.com/library/windows/hardware/dn236413)フィールド**ServiceInfo.xml**サービス メタデータ パッケージにします。 サービス メタデータ パッケージのスキーマについては、次を参照してください。[サービス メタデータ パッケージ スキーマ リファレンス](service-metadata-package-schema-reference.md)します。

  > [!NOTE]
  > これは、同じサービス数で指定した、**作成モバイル ブロード バンド エクスペリエンス ウィザード**Windows デベロッパー センターのダッシュ ボードでハードウェア。
  > モバイル ブロード バンドのアプリを作成していない場合は、組織の使用の GUID を生成できます。 どちらの場合は、常に、組織が発行するすべてのプロビジョニング ファイルを同じ GUID を使用する必要があります。

- [**サブスクライバー Id** ](https://msdn.microsoft.com/library/windows/apps/hh868305)組織内の顧客を一意に識別する文字列。 通信事業者の場合は、GSM 演算子 IMSI または ICCID 範囲またはプロバイダーの ID または CDMA 演算子のプロバイダー名があります。 通信事業者でない場合は、十分に一意の文字列を選択できます。

### <a name="activation"></a>ライセンス認証

デバイスのアクティブ化では、アクティブ化プロセスが、バック エンドに完了した後に発生します。 PC がネットワークに接続する前に特定の手順を実行する必要があります。 プロビジョニング エンジンでは、デバイスのアクティブ化要素で受信したアクティブ化の手順を使用します。 値が指定されていない場合は、クライアントの操作もする必要はありません。 使用可能なアクションは次のとおりです。

- **再接続**切断し、オペレーターのネットワークに接続します。

    **再登録**切断とオペレーターのネットワークに登録します。

- **データ**データや接続をアクティブ化するデバイスに送信する命令です。 プロビジョニング エンジンでは、デバイスには、このデータを渡します。 CDMA、この含めることができます指示など **\*228** OTA プログラミングのセッションを開始し、ネットワークに再接続します。

### <a name="mobile-broadband-information"></a>モバイル ブロード バンド情報

モバイル ブロード バンド情報には、いくつかの要素が含まれています。

[**MBNProfiles**](https://msdn.microsoft.com/library/windows/apps/hh868295)

通信事業者ネットワーク上のサブスクライバーの情報を定義します。 使用できる 2 つの異なるプロファイルがあります。

- [**PurchaseProfile**](https://msdn.microsoft.com/library/windows/apps/hh868301):新しいサブスクリプションを購入するオペレーターのネットワークに接続するために必要な情報です。

- [**DefaultProfile** ](https://msdn.microsoft.com/library/windows/apps/hh868290)すべてのモバイル ブロード バンド サブスクリプションは、ホーム ネットワーク オペレーターへの接続に使用される 1 つの既定のプロファイルを持つことができます。 Windows 接続マネージャーは、ネットワークに自動接続するため、このプロファイルを使用します。

    ```xml
    <MBNProfiles>
        <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
          <Name>Contoso MBN</Name>
          <Description>Contoso Mobile Broadband</Description>
          <HomeProviderName>Contoso MBN</HomeProviderName>
          <Context>
            <AccessString>contoso.com</AccessString>
            <UserLogonCred>
              <UserName>mbuser</UserName>
              <Password>mbpass</Password>
            </UserLogonCred>
          </Context>
        </DefaultProfile>
      </MBNProfiles>
    ```

[**ブランド化**](https://msdn.microsoft.com/library/windows/apps/hh868446)

> [!IMPORTANT]
> Windows 10 バージョン 1709 以降 ProvisioningAgent API によってプロビジョニングされたブランド化のフィールドはブランド COSA データベース内のフィールドで置き換えられました。 **ロゴ**は置き換えられました**ブランド アイコン**COSA でと**名前**代わられました**ブランド名**COSA でします。
>
> **ロゴ**と**名前**Windows 10 バージョン 1709 以降でプロビジョニングする場合と見なされなくします。 これらを使用すると、必要がありますを変更する場合は、ProvisioningAgent API に、エラーはスローされません**ブランド アイコン**と**ブランド名**COSA の代わりにします。  
>
> 詳細については**ブランド アイコン**と**ブランド名**を参照してください[デスクトップ COSA/APN データベースの設定 (デスクトップ COSA のみの設定)](desktop-cosa-apn-database-settings.md#desktop-cosa-only-settings)します。

Windows が、モバイル ブロード バンド ネットワークを表示する方法を指定することができますをブランド化します。 この情報は、存在する場合に、サービス メタデータをオーバーライドします。 情報が指定されていない場合は、サービス メタデータ パッケージの内容が使用されます。 ブランド化要素は次のとおりです。

- [**ロゴ**](https://msdn.microsoft.com/library/windows/apps/hh868460) Base64 でエンコードされました。PNG またはします。XML に埋め込まれている BMP ファイルです。 このロゴは、ネットワークの一覧に表示する場合は、モバイル ブロード バンド プロファイルに適用されます。

- [**名前**](https://msdn.microsoft.com/library/windows/apps/hh868463)モバイル ブロード バンド プロファイルの通信事業者の表示名を設定します。

#### <a name="sms-parsing"></a>SMS の解析

テキスト メッセージを識別およびプロビジョニング XML ファイルの一部として情報を抽出規則をプロビジョニングすることができます。 データ使用状況の統計を更新するか、プロビジョニング情報の更新を開始する、SMS メッセージを使用することができます。 これらのメッセージは、次の組み合わせによって識別できます。

- ベアラーの種類 (SMS/USSD)

- 送信者 (SMS のみ)

- 正規表現

SMS 通知の詳細については、次を参照してください。 [mobile operator notifications とシステム イベントを有効にする](enabling-mobile-operator-notifications-and-system-events.md)します。

各ルールには、次の情報が含まれています。

- **サイレント**メッセージの原因でこの値が true の場合、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベントのみです。 この値が false の場合、メッセージにより、 **SmsMessageReceived**イベント。

- **送信者が許可されている**が到着する元となる通知が許可されている予約済みのセンダのアドレスを指定します。 この数は、国際対応形式を含む SMS メッセージで受信する送信者数を正確に一致する必要があります。

- **パターン**正規表現を特定し、必要に応じて、テキスト メッセージからデータ フィールドを抽出します。 このパターンでは、送信者からのすべてのメッセージを一致します。 `[^]*`

- **RuleId**の一部として、モバイル ブロード バンド アプリに渡されるが、この規則の識別子、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント。 この識別子は、ルール、MobileOperatorNotification イベントをトリガーする SMS の原因となったし、メッセージを解析して、もう一度アプリの必要性を減らすことができますを知っているアプリを使用できます。

- **フィールドとグループ**正規表現パターン内の各キャプチャ グループが名前付きフィールドに関連付けられています。 これは、抽出し、使用可能な値のセットにデータを変換に使用されます。 最初の一致するグループを関連付けられるなど、**使用状況**フィールドと 2 番目の一致グループに結び付けることができます、 **UsageDataLimit**フィールド。 この関連付けは、最初の値が現在の使用状況情報、2 番目の値は最大使用量を示します。

  - **使用状況、UsagePercentage、UsageOverage、UsageOveragePercentage**:データの制限を超えた場合の数として、データの制限の割合としての絶対数として、またはデータの制限の割合としては、現在の使用量を表します。 絶対値では、値を表す単位を指定するグループを参照できます。

  - **UsageTimestamp**:日付と時間の使用法フィールドを計算します。 存在する場合はこの情報を含める必要がある**使用状況\\*** フィールドが含まれています。 書式指定文字列には、express、部分文字列を解釈する方法を次の識別子が含まれています。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>識別子</th>
    <th>説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%d</p></td>
    <td><p>10 進数による日 (01 ～ 31)</p></td>
    </tr>
    <tr class="even">
    <td><p>%H</p></td>
    <td><p>24 時間形式の時間 (00 ～ 23)</p></td>
    </tr>
    <tr class="odd">
    <td><p>%I</p></td>
    <td><p>12 時間形式 (01 ~ 12)</p></td>
    </tr>
    <tr class="even">
    <td><p>%m</p></td>
    <td><p>10 進数による月 (01 ～ 12)</p></td>
    </tr>
    <tr class="odd">
    <td><p>%M</p></td>
    <td><p>10 進数による分 (00 ～ 59)</p></td>
    </tr>
    <tr class="even">
    <td><p>%S</p></td>
    <td><p>10 進数による秒 (00 ～ 59)</p></td>
    </tr>
    <tr class="odd">
    <td><p>%y</p></td>
    <td><p>世紀なしの 10 進数による年 (00 ～ 99)</p></td>
    </tr>
    <tr class="even">
    <td><p>%Y</p></td>
    <td><p>年を 4 桁の 10 進数 (0000 ~ 9999)、</p></td>
    </tr>
    <tr class="odd">
    <td><p>%p</p></td>
    <td><p>午前/午後インジケーター</p></td>
    </tr>
    <tr class="even">
    <td><p>%#d、#H %、% #I %#m、#M %、%#S、%#y %#Y</p></td>
    <td><p>先行ゼロを付けないが、上記と同じ</p></td>
    </tr>
    </tbody>
    </table>

  - **DataLimit**:絶対に使用できる、ユーザーが許可されているバイト数これには、値を表す単位を指定するグループが含まれます。

  - **混雑 OverDataLimit**:ユーザーが、データの上限を超えたこと、負荷の高いネットワークが存在するかを示すアプリに報告するフラグを変更します。

  - **InboundBandwidth、OutboundBandwidth**:最大帯域幅の制限されている、ネットワーク、これと、値と単位を表すグループを指定します。

  - **PlanType**:ユーザーが将来の使用量に対する課金方法を指定します。

**注意**  だけで SMS メッセージを使用できる信頼されているため、SMS メッセージが Windows の動作に影響します。 センダのアドレスを制限することで、セキュリティが維持されます。 このセキュリティ メソッドでは、ネットワークの SMS ゲートウェイは、制限された送信者からのメッセージがスプーフィングされるにより前提としています。

### <a name="wi-fi-information"></a>Wi-fi 情報

このセクションでは、使用する Windows の Wi-fi ネットワーク プロファイルの任意の数を指定できます。 セクションの形式は、Windows ネイティブ WLAN API によって使用される XML スキーマに似ています。

> [!NOTE]
> その他のすべての設定が同じ場合、1 つのプロファイルは複数の Ssid を含めることができます。 (認証方法、暗号化の設定、プラン、およびなど) は、他の方法でさまざまなネットワークが異なる場合は、追加のプロファイルを作成する必要があります。

WLAN セクションを指定すると、コンピューターで構成される必要がありますすべてのプロファイルを指定する必要もあります。 それらのプロファイルでは、データ プランを参照するプランのセクションでは、含まれる必要があります。 このセクションが処理されるときに発生する動作は次のとおりです。

- コンピューターに、不要になったに指定されているプロファイルが削除されます。

- プロファイルを指定する場合、更新または作成します。

- 空の WLAN のセクションでは、すべてのプロファイルを削除します。

- 変更されていないコンピューターで WLAN プロファイルのまま WLAN セクションを省略するとします。

このセクションでは、追加のノードは、関連付けられているプランです。 このノードは、Windows に WLAN のプロファイルを関連付けるプラン セクションで説明されているプランを使用できます。 プランでは、ネットワークの使用状況測定の状態の Windows に通知し、コンピューターがネットワークに接続されている期間中に Windows の動作を制御することができます。

#### <a name="unencrypted-network-no-automatic-authentication"></a>暗号化されていないネットワーク、自動認証なし

このプロファイルは、オープン ネットワークへの接続に Windows を構成します。

- このネットワークに captive portal が含まれている場合は、ネットワークに接続するたびに、ブラウザーが開かれます。

- ネットワークに captive portal が含まれていない場合は、操作を行わなくても、ユーザーが接続されています。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
    </security>
  </MSM>
</WLANProfile>
```

#### <a name="unencrypted-network-wispr-authentication"></a>暗号化されていないネットワーク、WISPr 認証

このプロファイルでは、オープン ネットワークへの接続に Windows を構成し、ワイヤレス インターネット サービス プロバイダーがローミング (WISPr) 認証を使用します。

- ネットワークに WISPr 対応 captive portal が含まれている場合、指定されたユーザー名とパスワードが指定された認証サーバーに送信されます。

- Captive portal が WISPr の対応でない場合は、ネットワークに接続するたびに、ブラウザーが開かれます。

- ネットワークに captive portal が含まれていない場合は、操作を行わなくても、ユーザーが接続されています。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
        <UserName>WisprUser1</UserName>
        <Password>password1</Password>
        <TrustedDomains>
          <TrustedDomain>www.contosoportal.com</TrustedDomain>
        </TrustedDomains>
      </HotspotProfile>
    </security>
  </MSM>
</WLANProfile>
```

#### <a name="encrypted-network-eap-sim-authentication"></a>暗号化されたネットワーク、EAP SIM 認証

このプロファイルは、ホット スポット 2.0 ネットワークなど、認証の種類として、SIM を使用して、暗号化されたネットワークへの接続に Windows を構成します。 ホット スポット 2.0 では、EAP SIM 認証で WPA2-エンタープライズを使用する、このようなネットワークを定義します。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>WPA2</authentication>
        <encryption>AES</encryption>
        <useOneX>true</useOneX>
      </authEncryption>
      <OneX xmlns="http://www.microsoft.com/networking/OneX/v1">
        <EAcomputeronfig>
          <!-- The config XML for all EA methods can be found at: https://msdn.microsoft.com/library/cc232996(v=prot.10).aspx -->
          <EapHostConfig xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
            <EapMethod>
              <Type>18</Type>
              <VendorId>0</VendorId>
              <VendorType>0</VendorType>
              <AuthorId>311</AuthorId>
            </EapMethod>
            <Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
              <EapSim xmlns="http://www.microsoft.com/provisioning/EapSimConnectionPropertiesV1">
                <Realm Enabled="true"></Realm>
              </EapSim>
            </Config>
          </EapHostConfig>
        </EAcomputeronfig>
      </OneX>
    </security>
  </MSM>
</WLANProfile>
```

#### <a name="unencrypted-network-app-based-authentication"></a>暗号化されていないネットワーク、アプリ ベースの認証

このプロファイルは、オープン ネットワークに接続し、モバイル ブロード バンド アプリと連携 WISPr 認証を使用して Windows を構成します。

- ネットワークに captive portal が含まれている場合、アプリが WISPr 資格情報を提供するバック グラウンドで開かれます。 資格情報は、指定した認証サーバーに送信されます。

- Captive portal が WISPr の対応でない場合は、ネットワークに接続するたびに、ブラウザーが開かれます。

- ネットワークに captive portal が含まれていない場合は、操作を行わなくても、ユーザーが接続されています。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso WiFi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
        <ExtAuth>
          <ExtensionId>YourAppIdGoesHere</ExtensionId>
        </ExtAuth>
        <TrustedDomains>
          <TrustedDomain>www.contosoportal.com</TrustedDomain>
        </TrustedDomains>
      </HotspotProfile>
    </security>
  </MSM>
</WLANProfile>
```

### <a name="plan-information"></a>プラン情報

各モバイル ブロード バンドやホット スポットのプロファイルでは、プランを参照します。 複数のプロファイルには、同じプランを参照できます。 プランは個別の最上位レベルのセクションで説明します。

計画は 2 つのセクションに分かれています —*説明*と*使用状況*します。 これにより、最初にプロファイルとプロビジョニング ファイルが大きく、説明を提供し、顧客の現在の使用のみを含む小さいプロビジョニング ファイルを後で提供することができます。

この情報は、Windows の動作に直接影響するために使用され、ネットワークには、その動作を調整するアプリケーションに提供されます。 この情報は、ネットワーク情報 Api を使ってサード パーティ製アプリケーションに利用されることができます。

### <a name="description"></a>説明

一般に、顧客のサブスクリプションの期間にわたって低頻度で変更する要素を含みます。

- [**PlanType** ](https://msdn.microsoft.com/library/windows/apps/hh868468)演算子での顧客が請求関係の種類。

  - **無制限**使用状況では追加コストは発生しません。

  - **固定**ユーザーには、固定コストの使用量が割り当てられます。

  - **変数**ユーザーに基づいて使用量を支払います。

- [**SecurityUpdatesExempt** ](https://msdn.microsoft.com/library/windows/apps/hh868374)セキュリティがお客様による使用量にカウントを更新するかどうかを指定するブール値。

- [**DataLimitInMegabytes** ](https://msdn.microsoft.com/library/windows/apps/hh868367)ユーザーの場合、使用量が割り当てられた[ **PlanType** ](https://msdn.microsoft.com/library/windows/apps/hh868468)は**固定**します。

- [**BillingCycle** ](https://msdn.microsoft.com/library/windows/apps/hh868366)定義、プランの開始日付と時間、その継続時間、および請求サイクルの最後で何が発生します。

- [**BandwidthInKbps** ](https://msdn.microsoft.com/library/windows/apps/hh868343)としてネットワークで許可されているユーザーの接続を高速化; これは、そのプランでは、標準を反映または輻輳または過剰な使用 (最大 2 Gbps) のため、通信事業者による削減率が反映されます。

- [**MaxTransferSizeInMegabytes** ](https://msdn.microsoft.com/library/windows/apps/hh868371)準拠しているアプリケーションを許可するように使用されている接続の明示的なユーザーの承認がない場合、従量制課金接続を経由する個別のダウンロードのサイズを表す整数。

- [**UserSMSEnabled** ](https://msdn.microsoft.com/library/windows/apps/hh868376)ユーザー - SMS のサポートが、プランに含まれるかどうかを示します。 True の場合、Windows には、モバイル ブロード バンド インターフェイスが使用されていない場合でも、コネクト スタンバイのネットワークに接続されたデバイスが保持されます。 コンピューターがアイドル状態のとき、場合は false、Windows の電源の電源を節約するためにモバイル ブロード バンド インターフェイスがネットワークでアドレス指定可能なデバイスでないされいます。

### <a name="usage"></a>使用方法

次の要素は、高い頻度で変更できます。

- [**UsageInMegabytes** ](https://msdn.microsoft.com/library/windows/apps/hh868350)ユーザーの最新のデータ使用量。

- [**OverDataLimit** ](https://msdn.microsoft.com/library/windows/apps/hh868465)を示すブール値をユーザーが割り当てられた使用量を渡すかどうかを示す場合[ **PlanType** ](https://msdn.microsoft.com/library/windows/apps/hh868468)は**固定**します。

- [**混雑**](https://msdn.microsoft.com/library/windows/apps/hh868449)通常よりも低接続速度は過剰な使用により強制されているかどうかを示す、ブール値。 Congested フラグことを示します、ネットワークが、現在発生している (またはされると予想して)、負荷の高い優先順位の低い転送を可能であれば、別の時間まで延期する必要があります。 ピーク時間帯などの概念を示すために、オーバー ロードされたホット スポットに応答するか、このフラグを使用することができます。

### <a name="refresh"></a>Refresh

ネットワークの変更のため、またはテクニカル サポートについては、必要に応じて、コンピューターに更新された設定をプッシュできます。 Windows では、ユーザーやプロビジョニング API によって提供される情報を使用して定期的な更新を試行します。 更新は、演算子からの SMS 通知によってトリガーできます。 更新を有効にするには、プロビジョニング XML では、次の情報を提供する必要があります。

- [**TrustedCertificates** ](https://msdn.microsoft.com/library/windows/apps/hh868307)今後プロビジョニング ファイルの署名が信頼された証明書の拇印の一覧。

- [**DelayInDays** ](https://msdn.microsoft.com/library/windows/apps/hh868291) (整数) の数日前に、更新は行われません。

- [**RefreshURL** ](https://msdn.microsoft.com/library/windows/apps/hh868303)ユーザーの最新のコピーを取得するための HTTPS URL のファイルをプロビジョニングします。

- [**ユーザー名**](https://msdn.microsoft.com/library/windows/apps/hh868308) & [**パスワード**](https://msdn.microsoft.com/library/windows/apps/hh868297)再プロビジョニング ファイルを取得するときに、HTTP 認証を使用して、表示される省略可能な資格情報。 格納されている場合、この情報を暗号化する必要があります。

または、モバイル ブロード バンド アプリを提供できます、新しいファイルをプロビジョニング、いつでも、アプリとオペレーターのバックエンド間の通信に基づきます。

``` syntax
<RefreshParameters>
      <DelayInDays>30</DelayInDays>
      <RefreshURL>https://www.contoso.com/refresh</RefreshURL>
      <Username>foo</Username>
      <Password>bar</Password>
    </RefreshParameters>
```

### <a name="signature"></a>署名

プロビジョニング後、ユーザーが終了またはアプリをアンインストール後も維持されるシステムの設定を変更するので、検証のより厳密なメジャーはほとんどの Api よりも必要です。 この検証は、オペレーターの特定のハードウェア (SIM)、暗号署名、およびユーザーの確認の組み合わせによって提供されます。

プロビジョニングの要件:

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>SIM が存在するでしょうか。</th>
<th>プロビジョニングのソース</th>
<th>署名の要件</th>
<th>ユーザーの確認の要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい、MB プロバイダー</p></td>
<td><p>モバイル ブロード バンド アプリ</p></td>
<td><p>なし</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>はい、MB プロバイダー</p></td>
<td><p>演算子の web サイト</p></td>
<td><p>証明書が必要です。</p>
<ul>
<li><p>信頼されたルート CA にチェーン.</p></li>
<li><p>APN データベースでのモバイル ブロード バンド ハードウェアと関連付けるまたはメタデータが発生します。</p></li>
</ul></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>いいえ、Wi-fi プロバイダー</p></td>
<td><p>モバイル ブロード バンド appor web サイト</p></td>
<td><p>証明書が必要です。</p>
<ul>
<li><p>信頼されたルート CA にチェーンします。</p></li>
<li><p>拡張された検証のマークされます。</p></li>
</ul></td>
<td><p>ユーザーは、証明書が使用されます。 最初の時刻を確認するように求められます。確認は必要ありません以降です。</p></td>
</tr>
</tbody>
</table>

### <a name="permitted-combinations"></a>許可されている組み合わせ

[ **Global** ](https://msdn.microsoft.com/library/windows/apps/hh868294)は他のノードの特定の組み合わせは一般的なスキーマで必要なだけ最初のレベル ノードです。 このセクションでは、これらの一般的な組み合わせについて説明します。

- **プロファイル (WLANProfiles、MBNProfiles) + 説明と使用状況を含むプラン**情報およびそれぞれに現在の使用量の計画を作成または更新プログラムの完全なプロファイルの設定し、適用されます。 プロファイルが同じプロビジョニング ファイルで指定されていないプランを参照し、プロビジョニング ファイル内のプロファイルには、指定したプランが参照されていない場合に警告が返される場合は、エラーが返されます。

- **説明と (必要に応じて) の使用状況を含むプラン**既存の更新プログラムの計画情報がコンピューターで、プロファイルしますが、コンピューター上のプロファイルを変更しません。 コンピューターのプロファイルには、指定したプランが参照されていない場合は、警告が返されます。

- **プランの使用状況をのみ含む**コンピューターで、既存のプロファイルの使用状況情報を更新します。 ただし、プロファイルまたは各プロファイルに関連付けられているプランの説明を変更しません。

## <a name="common-scenarios"></a>一般的なシナリオ

プロビジョニングのメタデータを作成する必要がある一般的なシナリオを次に示します。

- [スキーマをプロビジョニングするアカウントを検索します。](#find-the-account-provisioning-schema)

- [デバイスにプロビジョニング XML を適用します。](#apply-provisioning-xml-to-the-device)

- [モバイル ブロード バンド ネットワークに自動的に接続するデバイスのプロビジョニング](#provision-the-device-to-connect-automatically-to-a-mobile-broadband-network)

- [Wi-fi ネットワークに自動的に接続するデバイスのプロビジョニング](#provision-the-device-to-connect-automatically-to-a-wi-fi-network)

- [WISPr が有効なホット スポットに自動的に接続するデバイスをプロビジョニングします。](#provision-the-device-to-connect-automatically-to-a-wispr-enabled-hotspot)

- [モバイル ブロード バンド デバイスにライセンス認証を送信します。](#sending-activation-to-the-mobile-broadband-device)

- [プロビジョニングが完了したら、ネットワークに再接続する場合は、モバイル ブロード バンド デバイスを強制します。](#force-the-mobile-broadband-device-to-reconnect-to-the-network-after-provisioning-completes)

- [接続プロファイルのデータ使用状況の統計を更新しています](#updating-data-usage-statistics-for-a-connection-profile)

- [SMS メッセージを使用してデータの使用状況を更新します。](#update-data-usage-by-using-an-sms-message)

### <a name="find-the-account-provisioning-schema"></a>スキーマをプロビジョニングするアカウントを検索します。

XSD スキーマで使用可能な **%systemroot%\\スキーマ\\プロビジョニング**Windows 8、Windows 8.1、または Windows 10 を実行している任意のコンピューターにします。

### <a name="apply-provisioning-xml-to-the-device"></a>デバイスにプロビジョニング XML を適用します。

モバイル ブロード バンド アプリを UWP アプリを使用して、または web サイトからプロビジョニング XML ファイルをデバイスに適用できます。

モバイル ブロード バンド アプリからプロビジョニングします。

1. インスタンスを作成、 [ **ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397)インスタンス (を使用して[ **Windows.Networking.NetworkOperators.ProvisioningAgent.CreateFromNetworkAccountId**](https://msdn.microsoft.com/library/windows/apps/br207398)).

2. 呼び出す[ **ProvisionFromXmlDocumentAsync**](https://msdn.microsoft.com/library/windows/apps/br207400)、符号なしのプロビジョニングの XML ドキュメントに渡します。

非同期操作の完了と、プロビジョニング操作の結果が返されます。

モバイル ブロード バンド アプリ以外の UWP アプリからプロビジョニングします。

1. 署名付きのアカウント プロビジョニング XML ドキュメントを生成します。

2. インスタンスを作成、 [ **ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397) (を既定のコンス トラクターを使用) のインスタンス。

3. 呼び出す[ **ProvisionFromXmlDocumentAsync**](https://msdn.microsoft.com/library/windows/apps/br207400)、署名の XML ドキュメントに渡します。

非同期操作が完了して、プロビジョニング操作の結果が返されます。

Web サイト: から

1. 署名付きのアカウント プロビジョニング XML ドキュメントを生成します。

2. 呼び出す[ **window.external.msProvisionNetworks**](https://msdn.microsoft.com/library/hh848316)、署名の XML ドキュメントに渡します。

操作が完了して、プロビジョニング操作の結果が返されます。

### <a name="provision-the-device-to-connect-automatically-to-a-mobile-broadband-network"></a>モバイル ブロード バンド ネットワークに自動的に接続するデバイスのプロビジョニング

使用してプロビジョニング XML ドキュメントを定義することができます、 **MBNProfile**セクション。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
    <Global>
        <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
        <SubscriberId>1234567890</SubscriberId>
    </Global>
    <MBNProfiles>
      <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
          <Name>Profile Name</Name>
          <Description>The Description</Description>
          <HomeProviderName>Contoso</HomeProviderName>
          <Context>
              <AccessString>apn</AccessString>
              <UserLogonCred>
                  <UserName>username</UserName>
                  <Password>password</Password>
              </UserLogonCred>
          </Context>
      </DefaultProfile>
    </MBNProfiles>
</CarrierProvisioning>
```

> [!NOTE]
> 子要素**DefaultProfile**が必要です。 詳細については、プロビジョニングの XML スキーマ リファレンスを参照してください。

### <a name="provision-the-device-to-connect-automatically-to-a-wi-fi-network"></a>Wi-fi ネットワークに自動的に接続するデバイスのプロビジョニング

使用してプロビジョニング XML ドキュメントを定義することができます、 **WlanProfiles**セクション。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <WLANProfiles>
    <WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
      <name>My Wi-Fi Hotspot</name>
      <SSIDConfig>
        <SSID>
          <name>wifihotspot1</name>
        </SSID>
      </SSIDConfig>
      <MSM>
        <security>
          <authEncryption>
            <authentication>open</authentication>
            <encryption>none</encryption>
            <useOneX>false</useOneX>
          </authEncryption>
        </security>
      </MSM>
    </WLANProfile>
  </WLANProfiles>
</CarrierProvisioning>
```

子要素**MSM**ネットワークに接続する方法を定義します。 これには、必要な EAP 構成が含まれます。 MSM 要素のすべての子要素、 [WLAN\_プロファイル スキーマ](https://msdn.microsoft.com/library/windows/desktop/ms707341)はサポートされています。 詳細については、プロビジョニングの XML スキーマ リファレンスを参照してください。

### <a name="provision-the-device-to-connect-automatically-to-a-wispr-enabled-hotspot"></a>WISPr が有効なホット スポットに自動的に接続するデバイスをプロビジョニングします。

ホット スポット認証を有効にする次の 2 つの方法のいずれかを使用できます。

1. 使用して資格情報を直接宣言、 **BasicAuth**ディレクティブ。

    ``` syntax
    <?xml version="1.0"?>
    <CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
      <WLANProfiles>
        <WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
          <name>Contoso Wi-Fi</name>
          <SSIDConfig>
            <SSID>
              <name>Contoso Wi-Fi</name>
            </SSID>
          </SSIDConfig>
          <MSM>
            <security>
              <authEncryption>
                <authentication>open</authentication>
                <encryption>none</encryption>
                <useOneX>false</useOneX>
              </authEncryption>
              <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
                <BasicAuth>
                  <UserName>Alice</UserName>
                  <Password>secret</Password>
                </BasicAuth>
                <TrustedDomains>
                  <TrustedDomain>hotspot.contoso.com</TrustedDomain>
                </TrustedDomains>
              </HotspotProfile>
            </security>
          </MSM>
        </WLANProfile>
      </WLANProfiles>
    </CarrierProvisioning>
    ```

2. 使用して認証用のアプリにリダイレクト、 **ExtAuth**ディレクティブ。

    ``` syntax
    <?xml version="1.0"?>
    <CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
      <WLANProfiles>
        <WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
          <name>Contoso Wi-Fi</name>
          <SSIDConfig>
            <SSID>
              <name>Contoso Wi-Fi</name>
            </SSID>
          </SSIDConfig>
          <MSM>
            <security>
              <authEncryption>
                <authentication>open</authentication>
                <encryption>none</encryption>
                <useOneX>false</useOneX>
              </authEncryption>
              <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
                <ExtAuth>
                  <ExtensionId>Alice</ExtensionId>
                </ExtAuth>
                <TrustedDomains>
                  <TrustedDomain>hotspot.contoso.com</TrustedDomain>
                </TrustedDomains>
              </HotspotProfile>
            </security>
          </MSM>
        </WLANProfile>
      </WLANProfiles>
    </CarrierProvisioning>
    ```

可能な場合の資格情報を直接定義する必要があります。 別のアプリへのリダイレクトは、電源と複雑性の影響を与えます。

### <a name="sending-activation-to-the-mobile-broadband-device"></a>モバイル ブロード バンド デバイスにライセンス認証を送信します。

内に含まれている任意バイナリ ラージ オブジェクト (BLOB)、 [ **CarrierSpecificData** ](https://msdn.microsoft.com/library/windows/apps/hh868447)要素は、ProvisioningAgent を使用して、Base64 でエンコードされた、デバイスへの送信を指定できます。 使用してこれを行う、**アクティベーション&lt;ServiceActivatation&gt;** プロビジョニング XML ディレクティブ。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <Activation>
    <ServiceActivation xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
      <CarrierSpecificData>YXJiaXRyYXJ5ZGF0YQ==</CarrierSpecificData>
    </ServiceActivation>
  </Activation>
</CarrierProvisioning>
```

このメソッドを呼び出すには、 [ **IMbnVendorSpecificOperation::SetVendorSpecific** ](https://msdn.microsoft.com/library/windows/desktop/dd323208)モバイル ブロード バンド API では、および BLOB の内容と共に SAFEARRAY を渡す方法です。

### <a name="force-the-mobile-broadband-device-to-reconnect-to-the-network-after-provisioning-completes"></a>プロビジョニングが完了したら、ネットワークに再接続する場合は、モバイル ブロード バンド デバイスを強制します。

モバイル ブロード バンド デバイス プロビジョニング後に、ネットワークに再接続を強制する 2 つの方法はあります。**ReregisterToNetwork**と**ReconnectToNetwork**します。

使用することができます、 **ReregisterToNetwork**モバイル ブロード バンド ラジオの電源を切ることによって、モバイル ブロード バンド ネットワークに強制的に再登録して、もう一度するディレクティブ。 オプションは、ある状態に復帰、既定のプロファイルを使用して、アダプターが接続されます。 このディレクティブを使用する必要があります限り注意、アカウントのアクティブ化した後、ネットワークから登録を解除する必要がある場合。

使用することができます、 **ReconnectToNetwork**ディレクティブとアカウントのアクティブ化が完了した後、コンテキストのアクティブ化は新しいセキュリティ ポリシーまたはポリシー設定を適用する必要があります。 これは、PDP コンテキストを非アクティブ化でし、モバイル ブロード バンド アダプターの既定のプロファイル設定に基づく再アクティブ化します。 同じプロビジョニング XML で既定のプロファイルが更新されると、新しいプロファイルの設定が使用されます。

必要に応じて、これらのディレクティブを使用して再試行カウント/間隔と、実行時間の遅延を指定できます。

> [!NOTE]
> ラジオが正常にリサイクルで場合、 **ReregisterToNetwork**既定のプロファイルを使用してネットワークに自動接続に失敗した場合、後続の再試行の無線をもう一度循環しない操作を行います。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <Activation>
      <!-- Cycle the radio and reconnect to the default profile with an 
           initial execution delay of 30 seconds and retries every 1 minute 
           up to 3 times.
           -->
      <ReregisterToNetwork
          xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1"
          Delay="PT30S"
          RetryCount="3"
          RetryInterval="PT1M"
          />
  </Activation>
</CarrierProvisioning>
```

### <a name="updating-data-usage-statistics-for-a-connection-profile"></a>接続プロファイルのデータ使用状況の統計を更新しています

使用してプロビジョニングしたプロファイルの使用状況を更新することができますのみ、 [ **ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397)プラン情報が更新されたファイルをプロビジョニングする新しいアカウントを適用することで。 使用状況の情報のみを含むプロビジョニング ファイルを提供したりできますのみプラン情報。 量に応じて、システム構成を変更する、新しいプロビジョニング ファイルは、次を含めることができます。

- プロファイル、プランの説明については、および使用状況

- 説明と使用状況 (既存のプロファイルを更新する) を計画します。

- プランの使用量 (既存のプロファイルとプランを更新)

新しいプロファイルと、XML で定義されていない参照プランを適用する場合、プロビジョニングの結果には、警告が含まれます。

### <a name="update-data-usage-by-using-an-sms-message"></a>SMS メッセージを使用してデータの使用状況を更新します。

これは、次の方法のいずれかで実現されます。

- オペレーターのメッセージを指定、演算子の通知メッセージが表示されるで SMS API を使用してメッセージを読み取るアプリでは、メッセージを解析およびを使用して、使用量を設定**IProvisionedProfile**します。

- 使用法フィールドの有効な組み合わせである演算子メッセージ ルールを指定し、直接、SMS で更新された使用量を指定します。

## <a name="troubleshooting"></a>トラブルシューティング

プロビジョニングの問題に遭遇した場合は、認識するため、次のセクションを使用できます。

### <a name="provisioning-api-results"></a>API の結果のプロビジョニング

プロビジョニングが失敗した場合、プロビジョニング操作を実行するときに例外を受け取ります。 例外が発生したエラーを以下に示します。

- プロビジョニング XML は準拠していない、 [CarrierControlSchema スキーマ](https://msdn.microsoft.com/library/windows/apps/hh868312)します。

- プロビジョニング XML は、シグネチャが必要ですが、適切に署名がありません。

### <a name="partial-provisioning-failures"></a>部分的なプロビジョニング エラー

プロビジョニング操作の一部のさまざまな理由により成功しません。 たとえば、プロビジョニング時に、Wi-fi ハードウェアへの参照があります。 プロビジョニング エージェントは、ファイル内のすべてのプロビジョニングを試行します。 プロビジョニングを使用して非同期的に返される結果が記載されて何かが失敗した場合、 [ **ProvisionFromXmlDocumentAsync**](https://msdn.microsoft.com/library/windows/apps/br207400)します。

結果は、XML としてが返され、障害を検出するために解析できます。 要素は、失敗の内容を表示する構造体を提供し、 **ErrorCode**属性は、標準的な HRESULT として失敗の理由を示します。

たとえば、WLAN のプロファイルがプロビジョニングされているありません、WLAN サービスがアクティブなため、次のエラー コードを示します。

``` syntax
<CarrierProvisioningResult>
    <WLANProfiles ErrorCode=”80070426”/>
</CarrierProvisioningResult>
```

個々 のプロファイルを適用できなかった場合に、次のように表示されます。

``` syntax
<CarrierProvisioningResult>
    <WLANProfiles>
        <WLANProfile Name=”MyProfile” ErrorCode=”80070005”/>
    </WLANProfiles>
</CarrierProvisioningResult>
```

### <a name="event-logs"></a>イベント ログ

内のイベント、 **Applications and Services Logs\\Microsoft\\Windows\\NetworkProvisioning\\Operational**チャネルでのプロビジョニングについての詳細なフィードバックを提供できますエラー。

### <a name="powershell-provisioningtesthelper-module"></a>PowerShell ProvisioningTestHelper モジュール

インポートすることができます、 **ProvisioningTestHelper**から Windows 8、Windows 8.1、および Windows 10 Sdk モジュール。 このモジュールを使用すると、生成し EV 証明書をインストール、インストールされた証明書を使用して XML ファイルに署名してプロビジョニングのスキーマに対して XML を検証します。 PowerShell セッションにモジュールをインポートするには、次のコマンドを入力します。

``` syntax
Import-Module "<path_to_sdk>\bin\<arch>\ProvisioningTestHelper.psd1"
```

場所&lt;*パス\_に\_sdk\\bin\\&lt;arch&gt;*  &gt; Windows 8、Windows 8.1 では、インストール場所は、またはコンピューターのアーキテクチャに対応する Windows 10 SDK。

このモジュールをインポートした後、次の 4 つの PowerShell コマンドレットを使用できます。

- **インストール TestEVCert**新しい CA 証明書を生成、EV SSL プロバイダーを信頼するには、テスト コンピューターに登録および生成しての署名に使用するため、EV 証明書をインストールすることを使用します。 証明書のインストールは、このコマンドレットを 1 回だけ実行する必要があります。 ファイルの任意の数は、証明書を使用してサインインできます。

    ``` syntax
    Install-TestEVCert -CertName <Certificate Name> -RootCertOutputPath <complete path to the folder to which the root certificate is to be exported>
    ```

    クライアント証明書が、コマンドで指定されている名前と、ルート証明書が"Root"と共に、クライアント証明書名が追加されます。 *- CertName*パラメーターは省略可能です。 – 証明書名パラメーターが指定されていない場合**MBAPTestCert**使用されます。

    *- RootCertOutputPath*パラメーターも省略可能です。 インストール RootCertFromFile コマンドレットを使用して別のコンピューターにインストールするルート証明書をエクスポートする場合に使用する必要があります。

- **インストール RootCertFromFile**テスト ルート証明書を開発コンピューター以外のコンピューターにクライアント エクスペリエンスをテストする別のコンピューターに適用されます。

    ``` syntax
    Install-RootCertFromFile -CertFile <complete path to the root certificate>
    ```

- **ConvertTo SignedXml** (テストの生成またはサード パーティ プロバイダーによって発行された) が EV 証明書を使用してプロビジョニング XML ファイルに、XML DSig 署名を適用します。 信頼された証明書からこの署名は、ハードウェアの関連で、モバイル ブロード バンド アプリから有効なものとしてプロビジョニング ファイルを受け入れるように Windows をによりします。

    ``` syntax
    ConvertTo-SignedXml -InputFile <complete path to the input XML file> -OutputFile <complete path to the output XML file> -CertName <name of the certificate used to sign the xml>
    ```

    このコマンドは入力 XML ファイルに署名、署名を XML ファイルに配置し、出力 XML ファイルに保存します。

- **テスト ValidProvisioningXml**プロビジョニング スキーマに対して、プロビジョニング XML (符号付きまたは符号なし) を検証します。

    ``` syntax
    Test-ValidProvisioningXml -InputFile <complete path to the input XML file>
    ```
