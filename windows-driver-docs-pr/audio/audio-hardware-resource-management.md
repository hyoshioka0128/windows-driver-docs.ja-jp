---
title: オーディオ ハードウェア リソースの管理
description: Windows 10 には、機能を使用して同時実行の制約を表現して、XML ファイルが含まれています。
ms.assetid: 6E94529E-F3F0-4DC5-AF8B-F896A4F991E3
ms.date: 10/29/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e3b7d4995110d9d998cbc02173a48693943b0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331466"
---
# <a name="audio-hardware-resource-management"></a>オーディオ ハードウェア リソースの管理

Windows 10 には、機能を使用して同時実行の制約を表現して、XML ファイルが含まれています。 リソースが制限されたモバイル デバイスで特定のオーディオ ストリームの優先順位を指定する機能は、カスタマー エクスペリエンスを強化できます。

**注**  このメカニズムは、携帯電話とタブレットで使用できるのみです。
 
低コストのモバイル デバイスでオーディオの良好なエクスペリエンスを作成する 1 つの課題は、一部のデバイスにさまざまな同時実行の制約があることです。 たとえば、2 のみをサポートするストリームをオフロードすると、デバイスが同時に最大 6 のオーディオ ストリームを再生のみできますです。 モバイル デバイスでアクティブな電話呼び出しがあるときに、デバイスが 2 つだけのオーディオ ストリームをサポートしていること。 デバイスでは、オーディオのキャプチャ時に、デバイスはのみに最大 4 つのオーディオ ストリームを再生できます。

Windows 10 には、優先度の高いオーディオ ストリームと携帯電話の呼び出しができるを再生することを保証する同時実行の制約を表現するためのメカニズムが含まれています。 システムが十分なリソースを持たない場合は、低優先度のストリームが終了します。 このメカニズムでは、携帯電話とタブレットではなくデスクトップやラップトップで使用できるのみです。

指定するには、制約は、これら 2 つの手順を完了します。

- 同時実行の制約の XML ファイルを作成する」の説明に従って[同時実行の制約の指定](#specify_concurrency_constraints)します。
- 」の説明に従って、カスタムの同時実行の制約の XML ファイルを使用するレジストリ エントリを構成する[レジストリ\_キー\_構成](#registry_key_configuration)します。

## <a name="span-idspecifyconcurrencyconstraintsspanspan-idspecifyconcurrencyconstraintsspanspan-idspecifyconcurrencyconstraintsspanspecify-concurrency-resource-constraints"></a><span id="Specify_Concurrency_Constraints"></span><span id="specify_concurrency_constraints"></span><span id="SPECIFY_CONCURRENCY_CONSTRAINTS"></span>同時実行リソースの制約を指定します。


制約の XML ファイルは 3 つのセクションに構成をされます。 必要な最初のセクションが定義されている&lt;制限&gt; &lt;制限/&gt;します。 このセクションでは、最大 15 個のリソース制約の定義に使用できます。 たとえば表示ストリームの最大数および読み込むことができるからストリームの最大数に対する制約を定義できます。

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

XML ファイルの次のセクションでは、2 つまたは複数のエンドポイントを格納している各リストを使用した、排他的なエンドポイントの 1 つまたは複数のリストを定義します。 これらをアクティブにできません同時にエンドポイントです。 このセクションは省略可能です。

たとえば、オーディオ ハードウェアに HandsetSpeaker と WiredHeadsetSpeaker を同時にアクティブでできない場合、同じ DAC にワイヤード (有線) の両方がある場合は、同じ ExclusiveEndpoints リストでこれらでなければなりません。

このセクションでは複数&lt;ExclusiveEndpoints&gt;ノード。 各 ExclusiveEndpoints ノードには、2 つ以上のエンドポイント ノードが含まれています。 エンドポイントの各ノードには、HWID、トポロジ名、および PinId が含まれています。

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

最後の必須 XML ファイルのセクションは、さまざまなリソースの消費量を定義します。 ここで、ファイルが複数含まれている&lt;ResourceConsumer&gt;エントリ。 各エントリは、リソース コンシューマーに関する情報を識別し、その関連リソースを使用します。 以前は、使用される各リソースに定義する必要があります、&lt;制限&gt;セクション。

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

オーディオのリソースが使用されるため、オーディオ、サービスは、リソースを追跡します。 リソース不足が使用できる場合は、低い優先度のストリームが終了したか、または既存のリソース コンシューマーが優先順位が高い場合は、現在のリソース要求が失敗しました。

次に、有効な&lt;ConsumerInfo&gt;エントリ。

-   &lt;PhoneCall&gt; - &lt;Phonecall&gt;ノードが含まれています、CallState 子ノードでは、「アクティブ」にある「保持」またはします。
-   &lt;Stream&gt; -オーディオのストリーム。 &lt;Stream&gt;ノードには、次の子ノードが含まれています。

    &lt;ドライバーの INF ファイルで指定されたリソース コンシューマーの HWID、ハードウェア ID (hw id)。

    &lt;TopologyName&gt; -リソース コンシューマーのトポロジ フィルター参照文字列。

    &lt;PinId&gt; -リソース コンシューマーの暗証番号 (pin) の ID。

    &lt;モード&gt;-関連付けられているモードの GUID。 詳細については、次を参照してください。[オーディオ信号の処理モード](audio-signal-processing-modes.md)します。

    &lt;ConnectorType&gt; -リソース コンシューマーのコネクタの種類。 有効な値は次のとおりです。ホスト、Loopback、またはオフロードします。

-   &lt;FM&gt;の FM ラジオします。
-   &lt;KeywordDetector&gt; -Cortana 音声の相互作用をサポートするために使用されるキーワードの検出機能。

次の表では、優先順位が最も高いものから表示されている、レンダリングのオーディオ ストリーム優先順位を示します。

|                          |     |
|--------------------------|-----|
| Communications           | 1   |
| ゲーム チャット                | 2   |
| スクリーン リーダー            | 3   |
| カメラのシャッター           | 4   |
| 話すプッシュします。             | 5   |
| 呼び出しの通知     | 6   |
| パーソナル アシスタント       | 6   |
| 音声認識                   | 7   |
| [着信音]                 | 8   |
| Alarm                    | 9   |
| ムービー                    | 10  |
| フォア グラウンドのみメディア    | 10  |
| バック グラウンドの可能なメディア | 11  |
| メディア                    | 11  |
| サウンド効果            | 12  |
| DTMF                     | 12  |
| ゲームのメディア               | 12  |
| System                   | 12  |
| ゲーム効果             | 12  |
| その他                    | 13  |
| アラート                   | 14  |

 

次の表では、優先順位が最も高いものから表示されているキャプチャ、オーディオ ストリーム優先順位を示します。

|                          |     |
|--------------------------|-----|
| Communications           | 1   |
| ゲーム チャット                | 2   |
| 話すプッシュします。             | 4   |
| パーソナル アシスタント       | 6   |
| 音声認識                   | 7   |
| バック グラウンドの可能なメディア | 8   |
| メディア                    | 8   |
| その他                    | 13  |
| ゲームのメディア               | 15  |
| スクリーン リーダー            | 15  |
| アラート                   | 15  |
| フォア グラウンドのみメディア    | 15  |
| ゲーム効果             | 15  |
| サウンド効果            | 15  |
| DTMF                     | 15  |
| 呼び出しの通知     | 15  |
| Alarm                    | 15  |
| カメラのシャッター           | 15  |
| ムービー                    | 15  |
| [着信音]                 | 15  |
| System                   | 15  |

 

**使用例**

- 例 1:ユーザーが Skype、通信のレンダリングとキャプチャのストリームを使用して通信が。 ゲーム効果ストリームを作成しようとしています。 ゲームを開始するとします。 十分なリソースが使用できない場合は、ゲーム効果ストリームの作成は失敗します。

- 例 2:ユーザーが音楽を再生します。 音声ストリームを作成するアプリケーションを起動します。 十分なリソースが使用できない場合は、音楽のストリームは終了し、音声ストリームの作成は成功します。

## <a name="span-idregistrykeyconfigurationspanspan-idregistrykeyconfigurationspanspan-idregistrykeyconfigurationspanregistry-key-configuration"></a><span id="Registry_Key_Configuration"></span><span id="registry_key_configuration"></span><span id="REGISTRY_KEY_CONFIGURATION"></span>レジストリ キーの構成

同時実行の制約の XML ファイルへの完全パスは、次のレジストリ キーで指定する必要があります。 

```inf
HKR\SYSTEM\MultiMedia\DeviceCapability\ResourceSettings\XMLConfig
```

ドライバーのインストールの相対パスです。 ドライバーの INF インストールで制約の XML ファイルはコピーする必要があるし、システムに登録する次の行が追加されます。

```inf
HKR,SYSTEM\MultiMedia\DeviceCapability\ResourceSettings\XMLConfig,<Name of the constraint>,,<Path to the constraint>
```

このレジストリ キーには、XML へのパスを含む値を提供します。 独自の XML ファイル内の制約のセットを提供するその他のサブシステム/オーディオ デバイスで潜在的なであるために、XML ファイルとレジストリ キーの値名の名前が一意であることをお勧めします。 レジストリ キーは、オーディオ ドライバーの INF ファイルで設定できます。


## <a name="span-idexamplexmlconstraintsfilespanspan-idexamplexmlconstraintsfilespanspan-idexamplexmlconstraintsfilespanexample-xml-constraints-file"></a><span id="Example_XML_Constraints_File"></span><span id="example_xml_constraints_file"></span><span id="EXAMPLE_XML_CONSTRAINTS_FILE"></span>XML の制約のファイルの例


これは、SYSVAD 仮想オーディオ ドライバーのサンプルから XML 制約ファイルの例です。

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

 

 




