---
title: WDI TLV generator/パーサー XML セマンティクス
description: TLV generator/パーサー XML ファイルは、メッセージ、コンテナー (TLVs)、およびプロパティグループ (構造体) の一覧です。 このトピックでは、XML 構文について説明します。
ms.assetid: AD268E68-B969-45D8-A2F2-4025E827D496
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f59ab54c77805620d7e7ad49812399faabe00f2
ms.sourcegitcommit: 97272cb572d24b1ac72669e51e5051089e1dd2c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84053282"
---
# <a name="wdi-tlv-generatorparser-xml-semantics"></a>WDI TLV generator/パーサー XML セマンティクス

TLV generator/パーサー XML ファイルは、メッセージ、コンテナー (TLVs)、およびプロパティグループ (構造体) の一覧です。 このトピックでは、XML 構文について説明します。

- [`<message />`](#message-)
  - [属性](#attributes)
  - [コンテンツ](#content)
  - [例](#example)
- [`<containerRef />`](#containerref-)
  - [属性](#containerref--attributes)
  - [コンテンツ](#container--contents)
  - [例](#containerref--example)
- [`<containers />`](#containers-)
- [`<container />`](#container-)
  - [属性](#container--attributes)
  - [Contents](#container--contents)
  - [例](#container--example)
- [`<groupRef />`](#groupref-)
  - [属性](#groupref--attributes)
  - [コンテンツ](#groupref--content)
  - [使用例](#groupref--examples)
- [`<namedType />`](#namedtype-)
  - [属性](#namedtype--attributes)
  - [コンテンツ](#namedtype--content)
  - [例](#namedtype--example)
- [`<aggregateContainer />`](#aggregatecontainer-)
  - [属性](#aggregatecontainer--attributes)
  - [コンテンツ](#aggregatecontainer--content)
  - [例](#aggregatecontainer--example)
- [`<propertyGroups />`](#propertygroups-)
- [プリミティブフィールド型 ( `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>` )](#primitive-field-types-bool-uint8-uint16-uint32-int8-int16-int32)
  - [属性](#attributes-for-primitive-field-types)
  - [Contents](#contents-for-primitive-field-types)
- [`<propertyGroup />`](#propertygroup-)
  - [属性](#propertygroup--attributes)
  - [Contents](#propertygroup--contents)
  - [例](#propertygroup--example)

## `<message />`

1つの最上位レベルの WDI メッセージを記述します。 これらのメッセージエントリに対してパーサー関数またはジェネレーター関数のみが存在します。

### <a name="attributes"></a>属性

- `commandId`-Dot11wdi で定義する必要があるシンボリック定数。
- `type`-コードに公開する型の名前 (パーサー/ジェネレーター関数を呼び出すときにこの型を使用します)。
- `description`-コマンドの説明。
- `direction`–このメッセージが、WDI から IHV ミニポートに移動するときに TLV ストリームに記述するかどうかを示します ("ToIhv" と呼ばれます)。また、IHV ミニポートから M0、M3、または M4 ("FromIhv" と呼ばれます) として WDI に向かう TLV ストリームを記述します。 「 [WDI TLV parser](wdi-tlv-parser-interface-overview.md)での*メッセージの方向*」の「インターフェイスの概要」を参照してください。

### <a name="content"></a>コンテンツ

コンテナー参照の一覧 ( `<containerRef />` )。 これらは、メッセージを構成する TLVs とは異なります。 これらは、セクションで定義されている型への参照です `<containers />` 。

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

`<container />`セクションで定義されているへの参照 `<containers />` 。

### <a name="containerref--attributes"></a>`<containerRef />`アトリビュート

- `id`-Wditypes で定義する必要がある TLV ID。
- `name`-親構造内の変数の名前。
- `optional`-省略可能なフィールドであるかどうかを指定します。 既定では false です。 生成されたコードは "省略可能" を適用します。
- `multiContainer`–生成されたコードが同じ型の複数の TLVs 想定する必要があるかどうかを指定します。 既定では false です。 False の場合、生成されたコードは1つだけが存在することを強制します。
- `type`-セクション内の特定の要素の "name" 属性への参照 `<containers />` 。
- `versionAdded`-バージョン管理の一部。 この TLV コンテナーが、この属性で示されているバージョンよりも小さいピアとの間で、バイトストリームに表示されないことを示します。
- `versionRemoved`-バージョン管理の一部。 この TLV コンテナーが、この属性で示されているもの以上のバージョンのピアとの間で、バイトストリームに表示されないことを示します。

### <a name="containerref--content"></a>`<containerRef />`情報

[なし] :

### <a name="containerref--example"></a>`<containerRef />` 「例」

```XML
<containerRef id="WDI_TLV_P2P_CHANNEL_NUMBER"
              name="ListenChannel"
              optional="true"
              type="WFDChannelContainer"/>
```

## `<containers />`

WDI メッセージで使用されるすべてのコンテナー/TLVs について説明します。 コンテナーは TLV バケットと見なすことができます。 型には、との2種類があり `<container />` `<aggregateContainer />` ます。

## `<container />`

1つの構造体参照または名前付きの型の TLV コンテナー。 静的にサイズ変更されますが、静的なサイズになっている限り、C スタイルの配列にすることができます。

### <a name="container--attributes"></a>`<container />`アトリビュート

- `name`-WDI メッセージ/その他のコンテナーによって参照される ID。
- `description`-コンテナーの内容についてのわかりやすい説明。
- `type`–コードに公開される型名。
- `isCollection`-生成されたコードが同じ TLV (C スタイル配列) 内の同じサイズ要素の多くを期待するかどうかを指定します。 既定値は false です (指定された型の1つの要素のみが想定されます)。
- `isZeroValid`-が true の場合にのみ有効 `isCollection` です。 ゼロ要素配列が許可されるかどうかを判断します。 これは、TLV ストリームが、存在しないオプションの TLV と存在するが、長さが 0 (Ssid など) であることを区別する必要がある場合に便利です。 この区別はまれであるため、既定値は false です。

### <a name="container--contents"></a>`<container />`内容

またはのいずれか `<groupRef />` `<namedType />` 。

### <a name="container--example"></a>`<container />` 「例」

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

セクションで定義されているプロパティグループ (構造体) への参照 `<propertyGroups />` 。

### <a name="groupref--attributes"></a>`<groupRef />`アトリビュート

- `name`-親構造内の構造体の名前。
- `ref`-セクション内の名前付き構造体への参照 `<propertyGroups />` 。
- `description`–構造が使用される対象のわかりやすい記述子。

### <a name="groupref--content"></a>`<groupRef />`情報

[なし] :

### <a name="groupref--examples"></a>`<groupRef />` 使用例

```XML
<container name="WFDChannelContainer"
           description="Container for a Wi-Fi Direct channel."
           type="WDI_P2P_CHANNEL_CONTAINER">
  <groupRef name="Channel"
            ref="WFDChannelStruct"
            description="Wi-Fi Direct Channel." />
</container>
```

## `<namedType />`

Wditypes または dot11wdi によって公開されている未加工の型への参照。 既定のシリアライザー (memcpy) を使用するため、埋め込みの問題のため、独自のリスクでを使用します。

### <a name="namedtype--attributes"></a>`<namedType />`アトリビュート

- `name`-親構造内の構造体の名前。
- `type`-実際のコードで使用する型名。
- `description`–構造がどのように使用されるかについてのわかりやすい説明。

### <a name="namedtype--content"></a>`<namedType />`情報

[なし] :

### <a name="namedtype--example"></a>`<namedType />` 「例」

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

さまざまなコンテナーの TLV コンテナー。 これは、入れ子になった TLVs を処理するために使用されます。

### <a name="-attributes"></a>`<aggregateContainer />`アトリビュート

- `name`-WDI メッセージ/その他のコンテナーによって参照される ID。
- `description`–コンテナーの内容についてのわかりやすい説明。
- `type`-コードに公開する型名。

### <a name="-content"></a>`<aggregateContainer />`情報

の一覧 `<containerRef />` 。

### <a name="-example"></a>`<aggregateContainer />` 「例」

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

すべてのコンテナーで使用されるすべての構造体について説明します。 構造体は、によって使用されるか `<container />` 、別の `<propertyGroup />` (入れ子になった構造体) によって参照されることがあります。 これらは、TLVs コンテナーとは別に定義されるため、再利用できます。 TLV ヘッダーはありません。

これらの定義は、構造を使用した埋め込みの問題を解決し、データを解釈する方法についてコードジェネレーターの指示を提供するために必要です。

>[!NOTE]
>ここでは順序が重要です。 すべてのデータオフセットは、プロパティグループの説明に基づいて暗黙的に指定され、ここで定義されている順序でデータが書き込まれ、解析されます。 これらの構造体はここで定義する必要があります。

## <a name="primitive-field-types-bool-uint8-uint16-uint32-int8-int16-int32"></a>プリミティブフィールド型 ( `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>` )

これらは、使用可能なプリミティブ型であり、生成されたコードによって適切に変換またはマーシャリングされます。

### <a name="attributes-for-primitive-field-types"></a>プリミティブフィールド型の属性

- `name`-親構造内のフィールド名。
- `description`–プロパティの内容についてのわかりやすい説明。
- `count`-指定されたプロパティの数。 既定値は1です。 1より大きい値を指定すると、このプロパティはコード内で静的にサイズ設定された配列になります。

### <a name="contents-for-primitive-field-types"></a>プリミティブフィールド型の内容

なし

## `<propertyGroup />`

個々の構造体。

### <a name="propertygroup--attributes"></a>`<propertyGroup />`アトリビュート

- `name`-WDI メッセージ/その他のコンテナーによって参照される ID。
- `description`–プロパティグループの内容についてのわかりやすい説明です。
- `type`-コードに公開する型名。

### <a name="propertygroup--contents"></a>`<propertyGroup />`内容

いくつかのプロパティの型 (構造体フィールド) を使用できます。

- `<bool/> <uint8/> <uint16/> <uint32/> <int8/> <int16/> <int32/>`

- `<groupRef />`

- `<namedType />`

### <a name="propertygroup--example"></a>`<propertyGroup />` 「例」

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
