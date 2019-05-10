---
title: WDI TLV ジェネレーター/パーサーの XML のセマンティクス
description: TLV ジェネレーター/パーサーの XML ファイルは、メッセージ コンテナー (TLVs) の一覧、プロパティは、(構造体) をグループ化します。 このトピックでは、XML 構文について説明します。
ms.assetid: AD268E68-B969-45D8-A2F2-4025E827D496
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7333a5f37d2b9c419daa513d0f2a19f6446fc824
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405276"
---
# <a name="wdi-tlv-generatorparser-xml-semantics"></a>WDI TLV ジェネレーター/パーサーの XML のセマンティクス


TLV ジェネレーター/パーサーの XML ファイルは、メッセージ コンテナー (TLVs) の一覧、プロパティは、(構造体) をグループ化します。 このトピックでは、XML 構文について説明します。

-   [`<message />`](#message-)
    -   [Attributes](#attributes)
    -   [コンテンツ](#content)
    -   [例](#example)
-   [`<containerRef />`](#containerref-)
    -   [Attributes](#attributes)
    -   [コンテンツ](#content)
    -   [例](#example)
-   [`<containers />`](#containers-)
-   [`<container />`](#container-)
    -   [Attributes](#attributes)
    -   [目次](#contents)
    -   [例](#example)
-   [`<groupRef />`](#groupref-)
    -   [Attributes](#attributes)
    -   [コンテンツ](#content)
    -   [使用例](#examples)
-   [`    <namedType />`](#namedtype-)
    -   [Attributes](#attributes)
    -   [コンテンツ](#content)
    -   [例](#example)
-   [`<aggregateContainer />`](#aggregatecontainer-)
    -   [Attributes](#attributes)
    -   [コンテンツ](#content)
    -   [例](#example)
-   [`<propertyGroups />`](#propertygroups-)
-   [フィールドのプリミティブ型 (`<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`)](#primitive-field-types-bool-uint8-uint16-uint32-int8-int16-int32)
    -   [Attributes](#attributes)
    -   [目次](#contents)
-   [`<propertyGroup />`](#propertygroup-)
    -   [Attributes](#attributes)
    -   [目次](#contents)
    -   [例](#example)

## `<message />`


1 つの最上位 WDI メッセージをについて説明します。 これらのメッセージのエントリのパーサー/ジェネレーター関数のみがあります。

### <a name="attributes"></a>属性

-   `commandId` -Dot11wdi.h で定義する必要がありますシンボリック定数。
-   `type` -(を使用するこの型パーサー/ジェネレーター関数を呼び出すときに) コードに公開される名前を入力します。
-   `description` -コマンドの説明。
-   `direction` – このメッセージに TLV ストリームがについて説明します ("ToIhv"と呼ばれます)、M1 の一部として IHV ミニポートに WDI から移動するとかどうかを示します、M0、M3、または ("FromIhv"といいます)、M4 として WDI に IHV ミニポートから移動するか (と呼ばれる、双方向の移動に TLV ストリームについて説明します "Both")。 参照してください*メッセージの方向*で[WDI TLV パーサー インターフェイスの概要](wdi-tlv-parser-interface-overview.md)します。

### <a name="content"></a>Content

コンテナーの参照の一覧 (`<containerRef />`)。 これらは、メッセージを構成するさまざまな TLVs です。 定義された型への参照は、`<containers />`セクション。

### <a name="example"></a>例

```XML
<message commandId="WDI_SET_P2P_LISTEN_STATE"
         type="WDI_SET_P2P_LISTEN_STATE_PARAMETERS"
         description="Parameters to set listen state."
         direction="ToIhv">
  <containerRef id="WDI_TLV_P2P_CHANNEL_NUMBER"
                name="ListenChannel"
                optional="true"
                type="WFDChannelContainer" />
  <containerRef id="WDI_TLV_P2P_LISTEN_STATE"
                name="ListenState"
                type="P2PListenStateContainer" />
</message>
```

## `<containerRef />`


参照を`<container />`で定義されている、`<containers />`セクション。

### <a name="attributes"></a>属性

-   `id` -TLV ID wditypes.h で定義する必要があります。
-   `name` -親構造体の変数の名前。
-   `optional` -オプションのフィールドがあるかどうかを指定します。 既定で false に設定します。 生成されたコードでは、「省略可能な特性」を適用します。
-   `multiContainer` – 生成されたコードが同じ型の複数の TLVs ことが予想されるかどうかを指定します。 既定で false に設定します。 False の場合、生成されたコードは、1 つだけが存在することを強制します。
-   `type` -特定の要素の"name"属性への参照、`<containers />`セクション。
-   `versionAdded` -バージョン管理の一部です。 この TLV コンテナーする必要がありますに表示されないことをバージョンのピアとの間のバイト ストリーム 1 より小さい、この属性に示されていることを示します。
-   `versionRemoved` -バージョン管理の一部です。 この TLV コンテナーが、この属性に示されている 1 つ以上のバージョンでのピアとの間のバイト ストリームに表示する必要がありますされないことを示します。

### <a name="content"></a>Content

なし。

### <a name="example"></a>例

```XML
<containerRef id="WDI_TLV_P2P_CHANNEL_NUMBER"
              name="ListenChannel"
              optional="true"
              type="WFDChannelContainer"/>
```

## `<containers />`


WDI メッセージで使用されるすべてのコンテナー/TLVs について説明します。 コンテナーは、TLV バケットを見なすことができます。 2 種類があります:`<container />`と`<aggregateContainer />`します。

## `<container />`


1 つの構造の参照または名前付きの型の TLV コンテナーです。 静的にサイズしますが、静的にサイズ設定されている限り、C スタイル配列があります。

### <a name="attributes"></a>属性

-   `name` -ID を WDI メッセージによって参照されている/その他のコンテナー。
-   `description` -(コンテナー) の項目の説明。
-   `type` – コードに公開される名前を入力します。
-   `isCollection` -を指定します生成されたかどうかのコードは同じ TLV (C スタイル配列) 内で同じサイズの要素の多くを想定する必要があります。 既定値は false (指定された型の 1 つの要素のみを想定)。
-   `isZeroValid` 唯一の有効な場合に`isCollection`は true。 0 の配列の要素が許可されているかどうかを判断します。 これは、TLV ストリームは、省略可能な TLV は 1 つと存在しないが存在するが、長さが 0 (Ssid) などを区別する必要がある場合に便利です。 この区別はまれであるため、既定値は false です。

### <a name="contents"></a>目次

いずれかの`<groupRef />`または`<namedType />`します。

### <a name="example"></a>例

```XML
<container name="P2PListenStateContainer"
           description="Container for P2P Listen State setting."
           type="WDI_P2P_LISTEN_STATE_CONTAINER">
  <namedType name="ListenState"
             type="WDI_P2P_LISTEN_STATE"
             description="P2P Listen State."/>
</container>
```

## `<groupRef />`


定義されたプロパティ グループ (構造体) への参照、`<propertyGroups />`セクション。

### <a name="attributes"></a>属性

-   `name` -親構造体の構造の名前。
-   `ref` -内の名前付き構造体への参照を`<propertyGroups />`セクション。
-   `description` – 構造体の使用フレンドリ記述子。

### <a name="content"></a>Content

なし。

### <a name="examples"></a>例

```XML
<container name="WFDChannelContainer"
           description="Container for a Wi-Fi Direct channel."
           type="WDI_P2P_CHANNEL_CONTAINER">
  <groupRef name="Channel"
            ref="WFDChannelStruct"
            description="Wi-Fi Direct Channel." />
</container>
```

## ` <namedType />`


Wditypes.hpp または dot11wdi.h により公開される生の型への参照。 使用する既定のシリアライザー (memcpy) ので、使用して、各自の責任でパディングの問題が原因です。

### <a name="attributes"></a>属性

-   `name` -親構造体の構造の名前。
-   `type` -実際のコードで使用する名前を入力します。
-   `description` – どのような構造の説明が使用されます。

### <a name="content"></a>Content

なし。

### <a name="example"></a>例

```XML
<container name="P2PListenStateContainer"
           description="Container for P2P Listen State setting."
           type="WDI_P2P_LISTEN_STATE_CONTAINER">
  <namedType name="ListenState"
             type="WDI_P2P_LISTEN_STATE"
             description="P2P Listen State."/>
</container>
```

## `<aggregateContainer />`


多くの異なるコンテナーの TLV コンテナーです。 これは、入れ子になった TLVs を処理するために使用されます。

### <a name="attributes"></a>属性

-   `name` -ID を WDI メッセージによって参照されている/その他のコンテナー。
-   `description` – (コンテナー) の項目の説明。
-   `type` -コードに公開される名前を入力します。

### <a name="content"></a>Content

一覧の`<containerRef />`します。

### <a name="example"></a>例

```XML
<aggregateContainer
    name="P2PInvitationRequestInfoContainer"
    type="WDI_P2P_INVITATION_REQUEST_INFO_CONTAINER"
    description="Generic container for Invitation Request-related containers.">
  <containerRef
    id="WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS"
    type="P2PInvitationRequestParamsContainer"
    name="RequestParams" />
  <containerRef
    id="WDI_TLV_P2P_GROUP_BSSID"
    type="MacAddressContainer"
    name="GroupBSSID"
    optional="true" />
  <containerRef
    id="WDI_TLV_P2P_CHANNEL_NUMBER"
    type="WFDChannelContainer"
    name="OperatingChannel"
    optional="true" />
  <containerRef
    id="WDI_TLV_P2P_GROUP_ID"
    type="P2PGroupIDContainer"
    name="GroupID" />
</aggregateContainer>
```

## `<propertyGroups />`


すべてのコンテナーで使用されるすべての構造について説明します。 構造体で使用できるか、 `<container />`、または別によって参照される`<propertyGroup />`(構造体を入れ子になった)。 再使用できるように TLVs コンテナーとは独立して定義されます。 TLV ヘッダーはありません。

これらの定義は構造体と埋め込みの問題を解決するのに役立つために必要なし、データの解釈方法については、コード ジェネレーターの手順を説明します。

**注**  順序が重要です。 プロパティ グループの説明に基づくすべてのデータ オフセットが含まれ、データはここで、定義した順序で記述された解析です。 ここで定義する必要はこれらの構造体。

 

## <a name="primitive-field-types-bool-uint8-uint16-uint32-int8-int16-int32"></a>フィールドのプリミティブ型 (`<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`)


これらは、使用可能なプリミティブ型であり、生成されたコードによって適切に変換/マーシャ リングは。

### <a name="attributes"></a>属性

-   `name` 親の構造体のフィールド名です。
-   `description` – のプロパティを説明します。
-   `count` の指定したプロパティの多く方法。 既定では、1 つです。 1 より大きい値では、このプロパティをコードに静的にサイズの配列にします。

### <a name="contents"></a>目次

なし

## `<propertyGroup />`


個別の構造体。

### <a name="attributes"></a>属性

-   `name` -ID を WDI メッセージによって参照されている/その他のコンテナー。
-   `description` – のプロパティ グループの説明。
-   `type` -コードに公開される名前を入力します。

### <a name="contents"></a>目次

いくつかの可能なプロパティの型 (構造体のフィールド) があります。

-   `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`

-   `<groupRef />`

-   `<namedType />`

### <a name="example"></a>例

```XML
<propertyGroup name="P2PDiscoverModeStruct"
               type="WDI_P2P_DISCOVER_MODE"
               description="Structure definition for P2P Discover Mode Parameters">
  <namedType name="DiscoveryType"
             type="WDI_P2P_DISCOVER_TYPE"
             description="Type of discovery to be performed by the port."/>
  <bool name="ForcedDiscovery"
        description="A flag indicating that a complete device discovery is required. If this flag is not set, a partial discovery may be performed." />
  <namedType name="ScanType"
             type="WDI_P2P_SCAN_TYPE"
             description="Type of scan to be performed by port in scan phase." />
  <bool name="ScanRepeatCount"
        description="How many times the full scan procedure should be repeated. If set to 0, scan should be repeated until the task is aborted by the host."/>
</propertyGroup>
<propertyGroup name="P2PDeviceInfoParametersStruct"
               type="WDI_P2P_DEVICE_INFO_PARAMETERS"
               description="Structure definition for P2P Device Information Parameters.">
  <uint8 count="6"
         name="DeviceAddress"
         description="Peer's device address." />
  <uint16 name="ConfigurationMethods"
          description="Configuration Methods supported by this device." />
  <groupRef name="DeviceType"
            description="Primary Device Type."
            ref="WFDDeviceType" />
</propertyGroup>
```

 

 





