---
title: オーディオ ハードウェア リソースの管理
description: Windows 10 には、と XML ファイルを使用して同時実行の制約を表現する機能が含まれています。
ms.assetid: 6E94529E-F3F0-4DC5-AF8B-F896A4F991E3
ms.date: 10/29/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9608a783fd0a1b19e51f204c03d4d7b587d62574
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999063"
---
# <a name="audio-hardware-resource-management"></a>オーディオ ハードウェア リソースの管理

Windows 10 には、XML ファイルを使用して同時実行の制約を表現する機能が含まれています。 リソースの制約付きモバイルデバイスでは、特定のオーディオストリームの優先順位を指定する機能によって、カスタマーエクスペリエンスを向上させることができます。

**注**  このメカニズムは、スマートフォンとタブレットでのみ使用できます。
 
低コストのモバイルデバイスで優れたオーディオエクスペリエンスを作成する際の1つの問題は、一部のデバイスでさまざまな同時実行制約があることです。 たとえば、デバイスが同時に最大6つのオーディオストリームを再生でき、2つのオフロードストリームのみをサポートする可能性があります。 モバイルデバイスにアクティブな通話がある場合、デバイスがサポートするオーディオストリームは2つだけである可能性があります。 デバイスがオーディオをキャプチャしている場合、デバイスは最大4つのオーディオストリームのみを再生できます。

Windows 10 には、高優先度のオーディオストリームや携帯電話通話を再生できるように、同時実行の制約を表現するメカニズムが含まれています。 システムに十分なリソースがない場合は、低優先度のストリームが終了します。 このメカニズムは、デスクトップやノート pc にない携帯電話やタブレットでのみ使用できます。

制約を指定するには、次の2つの手順を実行します。

- 「[同時実行制約を指定](#specify_concurrency_constraints)する」の説明に従って、同時実行制約 XML ファイルを作成します。
- 「 [\_レジストリキー\_の構成](#registry_key_configuration)」で説明されているように、カスタムの同時実行制約 XML ファイルを使用するようにレジストリエントリを構成します。

## <a name="span-idspecify_concurrency_constraintsspanspan-idspecify_concurrency_constraintsspanspan-idspecify_concurrency_constraintsspanspecify-concurrency-resource-constraints"></a><span id="Specify_Concurrency_Constraints"></span><span id="specify_concurrency_constraints"></span><span id="SPECIFY_CONCURRENCY_CONSTRAINTS"></span>同時実行リソースの制約を指定する


XML 制約ファイルは、3つのセクションで構成されています。 最初の必須セクションは、制限&lt;&gt; &lt;/制限&gt;によって定義されます。 このセクションは、最大15個のリソース制約を定義するために使用できます。 たとえば、レンダリングストリームの最大数とオフロードできるストリームの最大数に対する制約を定義できます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<ConstraintModel>
  
  <Limits> 
    <Resource>
      <ID>MaxRender</ID>
      <Consumption>6</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOffLoad</ID>
      <Consumption>2</Consumption>
    </Resource>
    ...

  </Limits>
```

XML ファイルの次のセクションでは、排他的なエンドポイントのリストを1つ以上定義します。各リストには2つ以上のエンドポイントが含まれています。 これらはエンドポイントで、同時にアクティブにすることはできません。 このセクションは省略可能です。

たとえば、オーディオハードウェアに、同じ DAC に対して接続されている [ExclusiveEndpoints Setスピーカ] と [Wiredヘッドホン] の両方があり、同時にアクティブにできない場合は、同じ [] の一覧に存在する必要があります。

このセクションには、 &lt;複数&gt;の ExclusiveEndpoints ノードを含めることができます。 各 ExclusiveEndpoints ノードには、2つ以上のエンドポイントノードが含まれています。 各エンドポイントノードには、HWID、名、および PinId が含まれています。

```xml
  <ExclusiveEndpoints>
    <Endpoint>
      <HWID>Root\sysvad_PhoneAudioSample</HWID>
      <!-- Example of h/w id specified in phoneaudiosample.inf -->
      <TopologyName>TopologySpeaker</TopologyName>
      <!-- Topology filter reference string-->
      <PinId>1</PinId>
      <!-- KSPIN_TOPO_LINEOUT_DEST -->
    </Endpoint>
    <Endpoint>
      <!-- Example of h/w id specified in phoneaudiosample.inf -->
      <HWID>Root\sysvad_PhoneAudioSample</HWID>
      <!-- Topology filter reference string-->
      <TopologyName>TopologyHandsetSpeaker</TopologyName>
      <!-- KSPIN_TOPO_LINEOUT_DEST -->
      <PinId>1</PinId>
    </Endpoint>
  </ExclusiveEndpoints>
```

XML ファイルの最後の必須セクションでは、さまざまなリソースコンシューマーを定義します。 ファイルのこのセクションには、 &lt;複数&gt;の ResourceConsumer エントリが含まれています。 各エントリは、リソースコンシューマーとそれに関連付けられているリソースに関する情報を指定します。 使用される各リソースは、 &lt;制限&gt;セクションで事前に定義されている必要があります。

```xml
  <ResourceConsumer>
    <!-- Active Phone call -->
    <ConsumerInfo>
      <PhoneCall>
        <CallState>Active</CallState>
      </PhoneCall>
    </ConsumerInfo>
    <Resource>
      <ID>MaxRender</ID>
      <Consumption>2</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOffLoad</ID>
      <Consumption>2</Consumption>
    </Resource>
    ...
  </ResourceConsumer>
```

オーディオリソースが使用されると、オーディオサービスはリソースを追跡します。 使用できるリソースが不足している場合は、優先順位の低いストリームが終了するか、既存のリソースコンシューマーの優先順位が高い場合は現在のリソース要求が失敗します。

これらは有効な&lt;ConsumerInfo&gt;エントリです。

-   &lt;PhoneCall&gt; - &lt;phonecall&gt;ノードには、"Active" または "Hold" を指定できる callstate 子ノードを含むが含まれています。
-   &lt;ストリーム&gt;オーディオストリーム。 ストリーム&lt;&gt;ノードには、次の子ノードが含まれています。

    &lt;HWID-ドライバーの INF ファイルで指定されているリソースコンシューマーのハードウェア ID (hw id)。

    &lt;名&gt; -リソースコンシューマーのトポロジフィルター参照文字列。

    &lt;PinId&gt; -リソースコンシューマーの pin id。

    &lt;Mode&gt; -関連付けられているモードの GUID。 詳細については、「[オーディオ信号処理モード](audio-signal-processing-modes.md)」を参照してください。

    &lt;ConnectorType&gt; -リソースコンシューマーのコネクタの種類。 有効な値は、Host、Loopback、または Offload です。

-   &lt;FM&gt; fm ラジオ。
-   &lt;KeywordDetector&gt; -Cortana 音声操作をサポートするために使用されるキーワード検出機能。

次の表は、オーディオストリームの優先順位が最も高い優先順位から順に表示されています。

|                          |     |
|--------------------------|-----|
| 通知           | 1   |
| ゲーム チャット                | 2   |
| スクリーン リーダー            | 3   |
| カメラシャッター           | 4   |
| 会話にプッシュ             | 5   |
| 通話通知で     | 6   |
| パーソナルアシスタント       | 6   |
| Speech                   | 7   |
| 着信音                 | 8   |
| アラーム                    | 9   |
| 映画                    | 10  |
| 前景のみのメディア    | 10  |
| バックグラウンド対応メディア | 11  |
| Media                    | 11  |
| サウンド効果            | 12  |
| DTMF                     | 12  |
| ゲームメディア               | 12  |
| システム                   | 12  |
| ゲーム効果             | 12  |
| その他                    | 13  |
| 警告                   | 14  |

 

次の表は、優先順位の高い順に一覧表示されるオーディオストリームの優先順位をまとめたものです。

|                          |     |
|--------------------------|-----|
| 通知           | 1   |
| ゲーム チャット                | 2   |
| 会話にプッシュ             | 4   |
| パーソナルアシスタント       | 6   |
| Speech                   | 7   |
| バックグラウンド対応メディア | 8   |
| Media                    | 8   |
| その他                    | 13  |
| ゲームメディア               | 15  |
| スクリーン リーダー            | 15  |
| 警告                   | 15  |
| 前景のみのメディア    | 15  |
| ゲーム効果             | 15  |
| サウンド効果            | 15  |
| DTMF                     | 15  |
| 通話通知で     | 15  |
| アラーム                    | 15  |
| カメラシャッター           | 15  |
| 映画                    | 15  |
| 着信音                 | 15  |
| システム                   | 15  |

 

**使用例**

- 例 1: ユーザーは、通信のレンダーストリームとキャプチャストリームを使用して、Skype を介して通信しています。 ゲームを開始し、ゲーム効果ストリームを作成しようとします。 使用可能なリソースが不足している場合、ゲーム効果ストリームの作成は失敗します。

- 例 2: ユーザーが音楽を再生している。 これらは、音声ストリームを作成するアプリケーションを起動します。 使用可能なリソースが不足している場合は、音楽ストリームが終了し、音声ストリームの作成は成功します。

## <a name="span-idregistry_key_configurationspanspan-idregistry_key_configurationspanspan-idregistry_key_configurationspanregistry-key-configuration"></a><span id="Registry_Key_Configuration"></span><span id="registry_key_configuration"></span><span id="REGISTRY_KEY_CONFIGURATION"></span>レジストリキーの構成

同時実行制約 XML ファイルへの完全なパスは、次のレジストリキーで指定する必要があります。 

```inf
HKR\SYSTEM\MultiMedia\DeviceCapability\ResourceSettings\XMLConfig
```

パスは、ドライバーのインストールに対する相対パスです。 ドライバー INF のインストールでは、制約 XML ファイルをコピーし、次の行を追加してシステムに登録する必要があります。

```inf
HKR,SYSTEM\MultiMedia\DeviceCapability\ResourceSettings\XMLConfig,<Name of the constraint>,,<Path to the constraint>
```

このレジストリキーに、XML へのパスを含む値を指定します。 XML ファイルの名前とレジストリ値の名前は一意にすることをお勧めします。他のサブシステムやオーディオデバイスでは、XML ファイルに独自の制約セットが提供される可能性があるためです。 レジストリキーは、オーディオドライバーの INF ファイルで設定できます。


## <a name="span-idexample_xml_constraints_filespanspan-idexample_xml_constraints_filespanspan-idexample_xml_constraints_filespanexample-xml-constraints-file"></a><span id="Example_XML_Constraints_File"></span><span id="example_xml_constraints_file"></span><span id="EXAMPLE_XML_CONSTRAINTS_FILE"></span>XML 制約ファイルの例


これは、SYSVAD 仮想オーディオドライバーサンプルの XML 制約ファイルの例です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<ConstraintModel>

  <Limits>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>3</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>2</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>2</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneLoopback</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>127</Consumption>
    </Resource>
  </Limits>

  <ExclusiveEndpoints>
    <Endpoint>
      <HWID>Root\sysvad_PhoneAudioSample</HWID>
      <!-- Example of h/w id specified in phoneaudiosample.inf -->
      <TopologyName>TopologySpeaker</TopologyName>
      <!-- Topology filter reference string-->
      <PinId>1</PinId>
      <!-- KSPIN_TOPO_LINEOUT_DEST -->
    </Endpoint>
    <Endpoint>
      <!-- Example of h/w id specified in phoneaudiosample.inf -->
      <HWID>Root\sysvad_PhoneAudioSample</HWID>
      <!-- Topology filter reference string-->
      <TopologyName>TopologyHandsetSpeaker</TopologyName>
      <!-- KSPIN_TOPO_LINEOUT_DEST -->
      <PinId>1</PinId>
    </Endpoint>
  </ExclusiveEndpoints>

  <ResourceConsumer>
    <!-- Phone call -->
    <ConsumerInfo>
      <PhoneCall>
        <CallState>Active</CallState>
      </PhoneCall>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>2</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneLoopback</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>26</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- FM -->
    <ConsumerInfo>
      <FM />
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- Keyword Detector -->
    <ConsumerInfo>
      <KeywordDetector />
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <!--Signal processing mode default-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, Communications mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{98951333-B9CD-48B1-A0A3-FF40682D73F7}</Mode>
        <!--Signal processing mode Communications-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, Speech mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{FC1CFC9B-B9D6-4CFA-B5E0-4BB2166878B2}</Mode>
        <!--Signal processing mode Speech-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, Notification mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{9CF2A70B-F377-403B-BD6B-360863E0355C}</Mode>
        <!--Signal processing mode Notification-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, Media mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{4780004E-7133-41D8-8C74-660DADD2C0EE}</Mode>
        <!--Signal processing mode Media-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, Movie mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}</Mode>
        <!--Signal processing mode Movie-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <!--Signal processing mode raw-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, default mode, offload -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <!--Signal processing mode default-->
        <ConnectorType>Offload</ConnectorType>
        <!-- Offload -->
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, Media mode, Offload -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{4780004E-7133-41D8-8C74-660DADD2C0EE}</Mode>
        <!--Signal processing mode Media-->
        <ConnectorType>Offload</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to speaker, Movie mode, offload -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}</Mode>
        <!--Signal processing mode Movie-->
        <ConnectorType>Offload</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>


  <ResourceConsumer>
    <!-- AudioStream to speaker, default mode, loopback -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <!--Signal processing mode default-->
        <ConnectorType>Loopback</ConnectorType>
        <!-- Loopback -->
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneLoopback</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, Communications mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{98951333-B9CD-48B1-A0A3-FF40682D73F7}</Mode>
        <!--Signal processing mode Communications-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, Speech mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{FC1CFC9B-B9D6-4CFA-B5E0-4BB2166878B2}</Mode>
        <!--Signal processing mode Speech-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, Notification mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{9CF2A70B-F377-403B-BD6B-360863E0355C}</Mode>
        <!--Signal processing mode Notification-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, Media mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{4780004E-7133-41D8-8C74-660DADD2C0EE}</Mode>
        <!--Signal processing mode Media-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, Movie mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}</Mode>
        <!--Signal processing mode Movie-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, default mode, offload -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <!-- Offload -->
        <ConnectorType>Offload</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, Media mode, Offload -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{4780004E-7133-41D8-8C74-660DADD2C0EE}</Mode>
        <!--Signal processing mode Media-->
        <ConnectorType>Offload</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to wired headset, Movie mode, offload -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}</Mode>
        <!--Signal processing mode Movie-->
        <ConnectorType>Offload</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>


  <ResourceConsumer>
    <!-- AudioStream to wired headset, default mode, loopback -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologySpeakerHeadset</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <!-- Loopback -->
        <ConnectorType>Loopback</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneLoopback</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to BT speaker, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyBthHfpSpeaker</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to BT speaker, raw mode, offload -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyBthHfpSpeaker</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <!-- Offload -->
        <ConnectorType>Offload</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxTwoOffload</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to BT speaker, default mode, loopback -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyBthHfpSpeaker</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <!-- Loopback -->
        <ConnectorType>Loopback</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneLoopback</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to handset speaker, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetSpeaker</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to handset speaker, Communications mode, host -->
    <ConsumerInfo>
      <Stream>
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <TopologyName>TopologyHandsetSpeaker</TopologyName>
        <!-- Topology filter reference string-->
        <PinId>1</PinId>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <Mode>{98951333-B9CD-48B1-A0A3-FF40682D73F7}</Mode>
        <!--Signal processing mode Communications-->
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to handset speaker, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetSpeaker</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream to handset speaker, default mode, loopback -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetSpeaker</TopologyName>
        <!-- KSPIN_TOPO_LINEOUT_DEST -->
        <PinId>1</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <!-- Loopback -->
        <ConnectorType>Loopback</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxThreeRender</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneLoopback</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicIn</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic, communications mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicIn</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode communications-->
        <Mode>{98951333-B9CD-48B1-A0A3-FF40682D73F7}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic, speech mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicIn</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode speech-->
        <Mode>{FC1CFC9B-B9D6-4CFA-B5E0-4BB2166878B2}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic, notification mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicIn</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode notification-->
        <Mode>{9CF2A70B-F377-403B-BD6B-360863E0355C}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicIn</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from wired headset mic, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicHeadset</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from wired headset mic, communications mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicHeadset</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode communications-->
        <Mode>{98951333-B9CD-48B1-A0A3-FF40682D73F7}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from wired headset mic, speech mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicHeadset</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode speech-->
        <Mode>{FC1CFC9B-B9D6-4CFA-B5E0-4BB2166878B2}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from wired headset mic, notification mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicHeadset</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode notification-->
        <Mode>{9CF2A70B-F377-403B-BD6B-360863E0355C}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from wired headset mic, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicHeadset</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic array, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicArray1</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic array, communications mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicArray1</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode communications-->
        <Mode>{98951333-B9CD-48B1-A0A3-FF40682D73F7}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic array, speech mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicArray1</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode speech-->
        <Mode>{FC1CFC9B-B9D6-4CFA-B5E0-4BB2166878B2}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic array, notification mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicArray1</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode notification-->
        <Mode>{9CF2A70B-F377-403B-BD6B-360863E0355C}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from mic array, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyMicArray1</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from BT mic, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyBthHfpMic</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from BT mic, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyBthHfpMic</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from handset mic, default mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetMic</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode default-->
        <Mode>{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from handset mic, communications mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetMic</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode communications-->
        <Mode>{98951333-B9CD-48B1-A0A3-FF40682D73F7}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from handset mic, speech mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetMic</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode speech-->
        <Mode>{FC1CFC9B-B9D6-4CFA-B5E0-4BB2166878B2}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from handset mic, notification mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetMic</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode notification-->
        <Mode>{9CF2A70B-F377-403B-BD6B-360863E0355C}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>2</Consumption>
    </Resource>
  </ResourceConsumer>

  <ResourceConsumer>
    <!-- AudioStream from handset mic, raw mode, host -->
    <ConsumerInfo>
      <Stream>
        <!-- Example of h/w id specified in phoneaudiosample.inf -->
        <HWID>Root\sysvad_PhoneAudioSample</HWID>
        <!-- Topology filter reference string-->
        <TopologyName>TopologyHandsetMic</TopologyName>
        <!-- KSPIN_TOPO_MIC_ELEMENTS -->
        <PinId>0</PinId>
        <!--Signal processing mode raw-->
        <Mode>{9E90EA20-B493-4FD1-A1A8-7E1361A956CF}</Mode>
        <ConnectorType>Host</ConnectorType>
      </Stream>
    </ConsumerInfo>
    <Resource>
      <ID>MaxTwoCapture</ID>
      <Consumption>1</Consumption>
    </Resource>
    <Resource>
      <ID>MaxOneRawStreamInPhoneCall</ID>
      <Consumption>1</Consumption>
    </Resource>
  </ResourceConsumer>

</ConstraintModel>
```

 

 




