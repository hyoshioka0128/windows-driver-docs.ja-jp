---
title: 通信事業者の通知イベントの技術的な詳細
description: 通信事業者の通知イベントの技術的な詳細
ms.assetid: 639f238a-4bb4-4ac0-9b59-92a761dbc351
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e25284f32fe27ffdd4379ec3c218045d1a7ad708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356926"
---
# <a name="mobile-operator-notification-event-technical-details"></a>通信事業者の通知イベントの技術的な詳細


このトピックでは、通信事業者の通知イベントの技術的な詳細を説明します。

-   [イベントのペイロード](#eventpl)

-   [メタデータを使用して MobileOperatorNotification イベントを登録します。](#regmd)

-   [プロビジョニング XML でのフィルタ リング規則を定義します。](#deffilter)

## <a name="span-ideventplspanspan-ideventplspanevent-payload"></a><span id="eventpl"></span><span id="EVENTPL"></span>イベントのペイロード


MobileOperatorNotification イベントのペイロードには、次のフィールドが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>[MessageType]</strong></p></td>
<td><p>イベントをトリガーしたメッセージの列挙体。</p></td>
</tr>
<tr class="even">
<td><p><strong>Interface</strong></p></td>
<td><p>イベントに関連付けられている物理インターフェイスに対応する GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EncodingType</strong></p></td>
<td><p>場合、メッセージのエンコード<strong>MessageType</strong>は SMS/USSD します。</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageDataSize</strong></p></td>
<td><p>サイズ (バイト単位)、メッセージの場合<strong>MessageType</strong> SMS/USSD です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>メッセージ</strong></p></td>
<td><p>未処理のメッセージを受信した場合に<strong>MessageType</strong> SMS/USSD です。</p></td>
</tr>
</tbody>
</table>

 

MobileOperatorNotification イベントにより、各シナリオで説明されている[通信事業者の通知シナリオ](mobile-operator-notification-scenarios.md)を使用してそれらを区別して、 **MessageType**イベント フィールドペイロード。 **MessageType**s は次のように列挙されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>列挙値</th>
<th>型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>GSM SMS</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>CDMA SMS</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>USSD</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>DataPlanThresholdReached</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>DataPlanReset</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>DataPlanDeleted</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p>ProfileConnected</p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>ProfileDisconnected</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>RegisteredRoaming</p></td>
</tr>
<tr class="even">
<td><p>9</p></td>
<td><p>RegisteredHome</p></td>
</tr>
<tr class="odd">
<td><p>10</p></td>
<td><p>TetheringEntitlementCheck</p></td>
</tr>
</tbody>
</table>

 

MobileOperatorNotification イベントに関連付けられている作業項目を効果的に差別化ロジックを開始する必要があります、 **MessageType**、シナリオごとに適切なコードを実行します。

### <a name="span-idgsmetcspanspan-idgsmetcspangsmcdma-sms-and-ussd"></a><span id="gsmetc"></span><span id="GSMETC"></span>GSM/CDMA SMS、USSD

SMS、USSD など、受信操作メッセージと共に、適切な対応する MobileOperatorNotification イベントをトリガーする**MessageType**秒。 これらの種類に固有では**EncodingType**、 **MessageDataSize**、および**メッセージ**します。

### <a name="span-iddataplanthresholdreachedspanspan-iddataplanthresholdreachedspanspan-iddataplanthresholdreachedspandataplanthresholdreached"></a><span id="DataPlanThresholdReached"></span><span id="dataplanthresholdreached"></span><span id="DATAPLANTHRESHOLDREACHED"></span>DataPlanThresholdReached

既定では、このメッセージの種類は無効です。 プロビジョニングのメタデータを指定するを使用して有効にすることができます、 [ **DataUsageInMobileOperatorNotificationEnabled** ](https://msdn.microsoft.com/library/windows/apps/hh868368)フィールドに、次のようにします。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{2c85b76b-f859-47c4-8122-721fe8b6c25f}</CarrierId>
    <SubscriberId>012345678901234</SubscriberId>
  </Global>
  <MBNProfiles>
    <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
      <Name>Contoso</Name>
      <AssociatedPlan>SamplePlan</AssociatedPlan>
      <Context>
        <AccessString>Contoso.com</AccessString>
        <UserLogonCred>
          <UserName>User</UserName>
          <Password>pass</Password>
        </UserLogonCred>
      </Context>
    </DefaultProfile>
  </MBNProfiles>
  <Plans>
    <Plan xmlns="http://www.microsoft.com/networking/CarrierControl/Plans/v1" Name="SamplePlan">
      <Description PlanType="Fixed">
        <DataLimitInMegabytes>500</DataLimitInMegabytes>
        <DataUsageInMobileOperatorNotificationEnabled>true</DataUsageInMobileOperatorNotificationEnabled>
      </Description>
    </Plan>
  </Plans>
</CarrierProvisioning>
```

アカウント プロビジョニングのメタデータに関する詳細については、次を参照してください。[アカウント プロビジョニング](account-provisioning.md)します。

このイベントが生成された**MessageType**ローカル データのカウンターがモバイル ブロード バンド インターフェイスでそので使用される (送受信されたバイト数) を推定するとき以降に変更されたを 5%、最後に見つかった、を除き、次の場合。

1.  データ プランの制限が指定されていない場合は、(ローミング)、ホーム ネットワークに接続されている、100 MB のローカル データの使用状況ごとにこのイベントがトリガーされます。

2.  ローミングのネットワークに接続している場合、データ プランの制限は適用されませんし、ローカル データ使用量の 5 MB のごとにこのイベントがトリガーされます。

Windows 8 でローカル データのカウンターは 1 分で更新されます。多くて、このイベントが説明されているすべてのシナリオで 1 分ごとに 1 回生成します。 Windows 8.1 のときにリアルタイムでイベントが配信される、5% のしきい値に達しています。

**注**  が、この情報は、良い第一級のガイドは、Windows ことはできませんアカウント未請求のトラフィックや使用状況の同じデータの上限は (ファミリの計画や SIM スワップ) を共有する他のデバイスにします。 通信事業者アプリは、ローカル データのカウンターを使用して、オペレーターの課金システムでは、前回の同期以降の使用量の概算のみにする必要があります。 既に処理されたデータ使用量の課金システムに従ってください。

 

### <a name="span-iddataplanresetspanspan-iddataplanresetspanspan-iddataplanresetspandataplanreset"></a><span id="DataPlanReset"></span><span id="dataplanreset"></span><span id="DATAPLANRESET"></span>DataPlanReset

プランのリセットの日付、データ使用量とサブスクリプション マネージャー (DUSM) は 0 に、ユーザーの現在のローカル データ使用量をリセットします。

### <a name="span-iddataplandeletedspanspan-iddataplandeletedspanspan-iddataplandeletedspandataplandeleted"></a><span id="DataPlanDeleted"></span><span id="dataplandeleted"></span><span id="DATAPLANDELETED"></span>DataPlanDeleted

固定の期限が事前有料データ プランの場合、DUSM が有効期限の日付に、アカウントに関連付けられている接続プロファイルを削除し、MobileOperatorNotification イベントがこれを使用してトリガーされた**MessageType**. 接続プロファイルが削除されると、Windows 接続マネージャーは不要になったに自動的に、接続プロファイルで説明されているネットワークに接続しようとします。

### <a name="span-idprofileconnectedandprofiledisconnectedspanspan-idprofileconnectedandprofiledisconnectedspanspan-idprofileconnectedandprofiledisconnectedspanprofileconnected-and-profiledisconnected"></a><span id="ProfileConnected_and_ProfileDisconnected"></span><span id="profileconnected_and_profiledisconnected"></span><span id="PROFILECONNECTED_AND_PROFILEDISCONNECTED"></span>ProfileConnected と ProfileDisconnected

これらの MobileOperatorNotification イベントが生成された**MessageType**s Windows 接続マネージャーは、オペレーターのエクスペリエンスのメタデータが提供するネットワーク プロファイルに接続するとき。 このイベントは、すべての接続上で発生し、切断、スリープ/再開に続く最初の接続を含みます。 デバイスが既に接続されている場合もトリガーされるアプリとサービスのメタデータをダウンロードしてインストールする場合。

ProfileConnected MessageType はモバイル ブロード バンド インターフェイスの L2 接続でトリガーされます。

**注**  ネットワーク id が完了する前に、このトリガーが発生します。 [ **NetworkStatusChanged** ](https://msdn.microsoft.com/library/windows/apps/br207299)イベント (の一部、 [ **NetworkInformation** ](https://msdn.microsoft.com/library/windows/apps/br207293) API) が生成されるときにネットワーク idネットワークの接続レベルを決定します。 ネットワーク id の詳細については、次を参照してください。[クイック スタート。ネットワーク接続情報の取得](https://msdn.microsoft.com/library/windows/apps/hh452990)と**NetworkInformation**クラス。

 

### <a name="span-idregisteredroamingandregisteredhomespanspan-idregisteredroamingandregisteredhomespanspan-idregisteredroamingandregisteredhomespanregisteredroaming-and-registeredhome"></a><span id="RegisteredRoaming_and_RegisteredHome"></span><span id="registeredroaming_and_registeredhome"></span><span id="REGISTEREDROAMING_AND_REGISTEREDHOME"></span>RegisteredRoaming と RegisteredHome

これらの MobileOperatorNotification イベントが生成された**MessageType**すると、Windows 接続マネージャーのローミングのネットワークに登録します。 このイベントは、次のスリープ/再開の初期登録を含む、すべての登録にトリガーされます。 アプリとサービスのメタデータをダウンロードしてインストールされているときに、デバイスがネットワークに登録されている既に場合もトリガーされます。

アプリでは、1 回はローミングのネットワークに登録すると、そのホーム ネットワークに戻ったときに 1 回のユーザーを通知する必要がありますのみです。 すべての登録でこのイベントがトリガーされるため、アプリのアプリのセッション データの前の登録済みの状態を追跡するための役目です。

### <a name="span-idtetheringentitlementcheckspanspan-idtetheringentitlementcheckspanspan-idtetheringentitlementcheckspantetheringentitlementcheck"></a><span id="TetheringEntitlementCheck"></span><span id="tetheringentitlementcheck"></span><span id="TETHERINGENTITLEMENTCHECK"></span>TetheringEntitlementCheck

この MobileOperatorNotification イベントが生成された**MessageType**すると、ユーザーがインターネット共有をオンにします。 ユーザーが、携帯電話会社が設定されている限り、インターネット共有を使用しようとしています。 たびにイベントがトリガーされた、 [AllowTethering](allowtethering.md)にサービス メタデータ スキーマ内の要素**EntitlementCheckRequired**します。 サービス メタデータのスキーマの詳細については、次を参照してください。[サービス メタデータ パッケージ スキーマ リファレンス](service-metadata-package-schema-reference.md)します。

アプリが携帯ネットワークでサポートされている適切な権利チェック メカニズムを実行しを使用して、結果をシステムに送信する必要があります、 [ **AuthorizeTethering** ](https://msdn.microsoft.com/library/windows/apps/dn266090)メソッド、の[ **NetworkOperatorNotificationEventDetails** ](https://msdn.microsoft.com/library/windows/apps/br207377)クラス、 [ **Windows.Networking.NetworkOperators** ](https://msdn.microsoft.com/library/windows/apps/br241148)名前空間。 携帯電話会社がサービス メタデータを変更する必要があります、アプリが権利チェックを実行する機能を持たない場合[AllowTethering](allowtethering.md)要素**常に**または**Never**、イベントは生成されません。

## <a name="span-idregmdspanspan-idregmdspanregister-for-the-mobileoperatornotification-event-by-using-metadata"></a><span id="regmd"></span><span id="REGMD"></span>メタデータを使用して MobileOperatorNotification イベントを登録します。


一般に、アプリが、ユーザーが作業項目をシステム イベント ブローカーに登録できる前に少なくとも 1 回実行してください。 ただし、MobileOperatorNotification イベントは、主要なモバイル ブロード バンド シナリオを完了に必要なために、このイベントは、サービス メタデータを使用してモバイル ブロード バンド アプリに関連付けられます。 サービス メタデータ、構成、 [DeviceCompanionApplications](devicecompanionapplications.md)要素。

``` syntax
<DeviceCompanionApplications>
  <Package>
    <Identity Name="MyOperatorNotification" Publisher="MyCorporation " />
    <Applications>
      <Application Id="MyOperatorNotification" />
        <DeviceNotificationHandlers>
          <DeviceNotificationHandler EventID="MobileOperatorNotificationHandler" EventAsset="backgroundtask.js" />
      </DeviceNotificationHandlers>
    </Applications>
  </Package>
</DeviceCompanionApplications>
```

**EventID**属性に、デバイスから想定されるイベントの種類をシステムに指示します。 値、 **EventAsset**属性は、バック グラウンド タスクを実装するエントリ ポイントを指す必要があります。 これにより、システムがその特定のイベントの発生時に実行するタスク。

この例を使用して、システムは作成し、そのデバイスに固有のイベントを登録します。 また、このイベント用のモバイル ブロード バンド アプリを登録します。 アプリはシステムによって実行するたびに、オペレーターへの通知を受信した backgroundtask.js という JavaScript ファイルが必要です。

モバイル ブロード バンド アプリが記述されている場合C#、イベントの資産が backgroundtask インターフェイスを実装するランタイム クラスをポイントする必要があります。

``` syntax
<DeviceNotificationHandlers>
  <DeviceNotificationHandler EventID="MobileOperatorNotificationHandler" EventAsset="MNOMessageBackground.OperatorNotification" />
```

サービスのメタデータとアプリをダウンロードすると、デバイスのセットアップ マネージャーは、アプリの実行前に、システム イベント ブローカーに適切な作業項目を登録します。 対応すると共に、MobileOperatorNotification イベントがトリガーされた後、作業項目を登録すると、モバイル ブロード バンド デバイスが登録されているか、ネットワークに接続されている場合は、すぐに**MessageType**します。

### <a name="span-idchangebackgroundtaskregistrationinmetadataspanspan-idchangebackgroundtaskregistrationinmetadataspanspan-idchangebackgroundtaskregistrationinmetadataspanchange-background-task-registration-in-metadata"></a><span id="Change_background_task_registration_in_metadata"></span><span id="change_background_task_registration_in_metadata"></span><span id="CHANGE_BACKGROUND_TASK_REGISTRATION_IN_METADATA"></span>メタデータでバック グラウンド タスクの登録を変更します。

バック グラウンド タスクのエントリ ポイントは、モバイル ブロード バンド アプリの更新バージョンで変更された場合、 [DeviceNotificationHandler](devicenotificationhandler.md)サービス メタデータ内の要素を変更することも必要があります。

サービス メタデータは、Windows 8、Windows 8.1、および Windows 10 を実行しているコンピューターに自動的に更新されます。 Microsoft Store では、モバイル ブロード バンド アプリが更新されます。 変更を避ける必要があります、 [DeviceNotificationHandler](devicenotificationhandler.md)サービス メタデータでタスクの登録をバック グラウンドします。 変更が必要な場合、サービス メタデータはすべて、別のバック グラウンド タスクのエントリ ポイントにモバイル ブロード バンドを更新していないユーザーのための機能を保持するために、モバイル ブロード バンドのアプリのサポートされている、すべてのバージョンで使用される参照を含める必要があります。アプリ。

## <a name="span-iddeffilterspanspan-iddeffilterspandefine-filtering-rules-in-provisioning-xml"></a><span id="deffilter"></span><span id="DEFFILTER"></span>プロビジョニング XML でのフィルタ リング規則を定義します。


Windows から XML ベースのプロビジョニング ファイルを受け入れます。 プロビジョニング XML のサンプル バージョンを次に示します。

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
    <Global>
        <!-- Adjust the Carrier ID to fit match the Service Number in service metadata. Refer to the documentation about CarrierId. -->
        <CarrierId>{11111111-1111-1111-1111-111111111111}</CarrierId>
        <!-- Adjust the Susbscriber ID. Refer to the documentation about Subscriber ID's. -->
        <SubscriberId>1234567890</SubscriberId>
    </Global>
    <MBNProfiles>
        <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
            <!-- Adjust the profile name -->
            <Name>Contoso</Name>
          <AssociatedPlan>Limited</AssociatedPlan>
            <!-- Adjust the home provider name for the given SIM/Device -->
            <HomeProviderName>Contoso</HomeProviderName>
            <Context>
                <!-- Adjust the access string to your APN. -->
                <AccessString>Contoso.Contoso</AccessString>
                <!-- Adjust the UserLogonCred to fit your UserLogonCred. Refer to the documentation about UserLogonCred's. -->
                <UserLogonCred>
                    <UserName>user</UserName>
                    <Password>password</Password>
                </UserLogonCred>
            </Context>
        </DefaultProfile>
      <Messages xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
        <Message RuleId="Sample1" Silent="true">
          <SMSBearer ClassZeroOnly="false" Sender="18005551212"/>
          <!-- [^]* matches all messages from this sender, regardless of content -->
          <Pattern>[^]*</Pattern>
          <!-- Because no Fields are specified, this message will be passed to the operator app without parsing. -->
        </Message>
        <Message RuleId="Sample2" Silent="false">
          <!-- Parsing a simple usage message. -->
          <USSDBearer/>
          <Pattern>(\d+\.\d+)(\w+) of (\d+)(\w+) used as of (\S+)</Pattern>
          <!-- Using these field definitions, Windows will automatically update usage data before passing the message
               to the operator app. -->
          <Units G="GB" M="MB"/>
          <Fields>
            <!-- These fields are currently unordered, but an order will be required in RC. -->
            <Usage Group="1" UnitGroup="2"/>
            <UsageTimestamp Group="5" Format="%I:%M%p on %d %b"/>
            <DataLimit Group="3" UnitGroup="4"/>
          </Fields>
        </Message>
      </Messages>
  </MBNProfiles>
  <Provisioning /> 
</CarrierProvisioning>
```

アカウント プロビジョニングのメタデータに関する詳細については、次を参照してください。[アカウント プロビジョニング](account-provisioning.md)します。

演算子メッセージは、この XML で定義できるように、テキスト メッセージを識別するルール。

-   **送信者が許可されている**送信者の属性が到着する元となる通知が許可されている予約済みのセンダのアドレスを指定します。 (この数する必要がありますと正確に一致国際対応形式を含む SMS メッセージで受信する送信者数)。

-   **パターン**正規表現を特定し、必要に応じて、テキスト メッセージからデータ フィールドを抽出します。 送信者からのすべてのメッセージを一致させるのには、パターンを使用して`[^]*`します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Mobile operator notifications とシステム イベントを有効にします。](enabling-mobile-operator-notifications-and-system-events.md)

[作成とインターネットの共有エクスペリエンスの構成](creating-and-configuring-internet-sharing-experiences.md)

 

 






