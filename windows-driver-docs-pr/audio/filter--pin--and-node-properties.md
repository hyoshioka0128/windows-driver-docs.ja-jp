---
title: フィルター、ピン、ノードのプロパティ
description: フィルター、ピン、ノードのプロパティ
ms.assetid: e0d52e97-459f-4095-9cf5-1474117ce66a
keywords:
- オーディオプロパティ WDK、フィルター
- WDM オーディオプロパティ WDK、フィルター
- オーディオプロパティ WDK、pin
- WDM オーディオプロパティ WDK、pin
- オーディオプロパティ WDK、ノード
- WDM オーディオプロパティ WDK、ノード
- フィルターのプロパティ WDK audio
- ノードのプロパティ WDK audio
- KS WDK オーディオ、プロパティ要求をフィルター処理します
- WDK オーディオ、プロパティ要求をフィルター処理します
- WDK オーディオのフィルター、プロパティの概要
- ノード WDK オーディオ、プロパティの概要
- WDK オーディオのピン留めプロパティの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 237d5016a6d16a6781fb999466c341564b69bbdb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831239"
---
# <a name="filter-pin-and-node-properties"></a>フィルター、ピン、ノードのプロパティ


## <span id="filter_pin_and_node_properties"></span><span id="FILTER_PIN_AND_NODE_PROPERTIES"></span>


Microsoft Windows Driver Model (WDM) オーディオドライバーは、オーディオデバイスを KS フィルターとして表し、デバイス上のハードウェアバッファーをフィルターのピンとして表します。 クライアントがこれらのフィルターオブジェクトまたはピンオブジェクトのいずれかにプロパティ要求を送信すると、ポートドライバーは要求を受信し、ポートドライバーまたはミニポートドライバーの適切なプロパティハンドラーに要求をルーティングします。

オーディオデバイスは、次の3種類のプロパティをサポートしています。

-   **フィルターのプロパティ**

    フィルタープロパティは、フィルター内の特定のピンまたはノードのプロパティではなく、全体としてのフィルターのプロパティです。 フィルタープロパティの要求ではフィルターハンドルが指定されていますが、ノード Id が指定されていません。

-   **Pin のプロパティ**

    Pin プロパティは、フィルターの特定のピンインスタンスのプロパティです。 これらのプロパティの要求ではピンハンドルが指定されていますが、ノード Id は指定されていません。

-   **ノードのプロパティ**

    ノードプロパティは、フィルター内のトポロジノードのプロパティです。 ノードプロパティの要求では、フィルターハンドルまたはピンハンドル、およびノード ID が指定します。

ノードプロパティの要求がフィルターハンドルとピンハンドルのどちらを指定するかは、ノードがフィルターに固有であるかどうかによって異なります。 詳細については、次の「ノードのプロパティ」を参照してください。

次の図は、この3種類のプロパティ要求を示しています。 pin インスタンスに送信されたピンプロパティ要求、ノードに送信されたノードプロパティ要求 (フィルターまたは pin インスタンス)、フィルタープロパティ要求がフィルターインスタンスに送信されたものです。

![フィルター、ピン、およびノードプロパティの要求を示す図](images/propreqs.png)

通常、ポートドライバーは、フィルターおよび pin プロパティに対するほとんどの要求を処理し、ミニポートドライバーはノードプロパティの要求を処理します。

ポートドライバーは、 [sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)によって使用されるフィルターおよび pin プロパティ用の独自の組み込みハンドラーを提供します (「 [ksk Propsetid\_Sysaudio](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-sysaudio)および[kspropsetid\_sysaudio\_Pin](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-sysaudio-pin))」および「WDMAud」を参照してください。 [システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)。 ミニポートドライバーは、ポートドライバーが処理するプロパティのハンドラーを実装する必要はありません。 一般的なミニポートドライバーでは、フィルターおよび pin プロパティのハンドラーがいくつか提供されています。 ミニポートドライバーは、オーディオデバイスのハードウェアに依存する機能を表すノードプロパティのハンドラーを提供します。 ポートドライバーは、ノードプロパティの組み込み処理を提供しません。ただし、 [**Ksk プロパティ\_トポロジ\_名**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-name)は例外です。

ポートドライバーとミニポートドライバーの両方が同じプロパティのハンドラーを提供する場合、ポートドライバーは独自のハンドラーを使用し、ミニポートドライバーのハンドラーを無視します。

### <a name="span-idfilter_descriptorsspanspan-idfilter_descriptorsspanspan-idfilter_descriptorsspanfilter-descriptors"></a><span id="Filter_Descriptors"></span><span id="filter_descriptors"></span><span id="FILTER_DESCRIPTORS"></span>フィルター記述子

ポートドライバーは、 [**IMiniport:: GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)メソッドを呼び出すことによって、ミニポートドライバーのプロパティハンドラーへのポインターを取得します。 このメソッドを使用して、ポートドライバーは、 [**pcfilter\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)型の構造であるミニポートドライバーのフィルター記述子へのポインターを取得します。 この構造体は、フィルタ、ピン、およびノードのプロパティに対応するミニポートドライバーのプロパティハンドラーを指定します。

-   PCFILTER\_記述子構造体の**AutomationTable**メンバーは、フィルターのオートメーションテーブルをポイントします。 次の表では、フィルターのプロパティに対応するミニポートドライバーのプロパティハンドラーを指定します。

-   PCFILTER\_記述子構造体の**ピン**メンバーには、ピンのオートメーションテーブルが含まれています。 各テーブルは、特定の pin の種類のピンプロパティのプロパティハンドラーを指定します。

-   PCFILTER\_記述子構造体の**nodes**メンバーには、フィルター内のトポロジノードのオートメーションテーブルが含まれています。 各テーブルには、特定のノード型のノードプロパティのプロパティハンドラーが指定されています。

### <a name="span-idfilter_propertiesspanspan-idfilter_propertiesspanspan-idfilter_propertiesspanfilter-properties"></a><span id="Filter_Properties"></span><span id="filter_properties"></span><span id="FILTER_PROPERTIES"></span>フィルターのプロパティ

ポートドライバーは、PCFILTER\_記述子の**AutomationTable**メンバーを介して、ミニポートドライバーのフィルタープロパティハンドラーにアクセスします。 通常、このオートメーションテーブルにはいくつかのハンドラーが含まれています。これは、ポートドライバーが、SysAudio と WDMAud がオーディオデバイスのクエリと構成に使用するすべてのフィルタープロパティ用に独自の組み込みハンドラーを提供するためです。

ただし、ミニポートドライバーは、ポートドライバーで使用できないハードウェアに依存する情報を提供する[**Ksk プロパティ\_GENERAL\_COMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-general-componentid)などのフィルタープロパティのハンドラーを提供できます。 Microsoft Windows Driver Kit (WDK) の2つのサンプルオーディオドライバーは、KSK プロパティ\_GENERAL\_COMPONENTID プロパティを処理します。 詳細については、Msvad および Sb16 サンプルのミニポートドライバーの実装に関する説明を参照してください。

Portcls のすべてのポートドライバーは、 [Ksk propsetid\_ピン](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)および[kspropsetid\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)プロパティセットの処理を提供します。 これらのセットのすべてのプロパティはフィルタープロパティです。ただし、 [**Ksk プロパティ\_トポロジ\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-name)は例外です。これは、ノードプロパティです。これは、要求のターゲットを指定するために、ピンハンドルではなくフィルターハンドルを使用します。 ポートドライバーは、次のような KSK PROPSETID\_ピンプロパティのサブセットをサポートしています。

[**KSK プロパティ\_ピン\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-category)

[**KSK プロパティ\_ピン\_CINSTANCES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-cinstances)

[**KSK プロパティ\_PIN\_通信**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-communication)

[**KSK プロパティ\_PIN\_CONSTRAINEDDATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)

[**KSK プロパティ\_ピン\_CTYPES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-ctypes)

[**KSK プロパティ\_ピン留め\_データフロー**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataflow)

[**KSK プロパティ\_ピン\_DATAINTERSECTION 集合**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)

[**KSK プロパティ\_PIN\_DATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)

[**KSK プロパティ\_\_GLOBALCINSTANCES にピン留めする**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-globalcinstances)

[**KSK プロパティ\_ピン留め\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-interfaces)

[**KSK プロパティ\_ピン\_メディア**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-mediums)

[**KSK プロパティ\_PIN\_名**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-name)

[**KSK プロパティ\_PIN\_NECESSARYINSTANCES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-necessaryinstances)

[**KSK プロパティ\_固定\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)

[**KSK プロパティ\_PIN\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)

[**KSK プロパティ\_PIN\_PROPOSEDATAFORMAT2**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat2)

これらのプロパティは、フィルターに属するピンファクトリに関する情報を提供します。 通常、クライアントは、pin インスタンスを作成する前に、これらのプロパティのフィルターに対してクエリを実行します。 ポートドライバーは、フィルターの内部トポロジに関する情報を提供する、すべての KSPROPSETID\_トポロジプロパティをサポートしています。

さらに、DMus ポートドライバーは、 [ **\_の Ksk プロパティのハンドラー\_MASTERCLOCK**](https://docs.microsoft.com/previous-versions/ff537403(v=vs.85))プロパティを提供します。これは、DirectMusic フィルターの取得専用プロパティです。 KSK プロパティ\_シンセサイザー\_MASTERCLOCK は、 [Kspropsetid\_SynthClock](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synthclock)プロパティセットのメンバーです。

### <a name="span-idpin_propertiesspanspan-idpin_propertiesspanspan-idpin_propertiesspanpin-properties"></a><span id="Pin_Properties"></span><span id="pin_properties"></span><span id="PIN_PROPERTIES"></span>Pin のプロパティ

ポートドライバーは、PCFILTER\_記述子の**ピン**メンバーを介して、ミニポートドライバーのピンプロパティハンドラーにアクセスします。 このメンバーは、ピン記述子の配列を指します。各記述子は、ピンの種類のオートメーションテーブルを指します (pin ID によって識別されます。これは単なる配列インデックスです)。

通常、これらのオートメーションテーブルには、SysAudio と WDMAud が使用するすべての pin プロパティに独自のハンドラーが用意されているため、いくつかのエントリが含まれています。 ミニポートドライバーには、ポートドライバーで処理されない1つ以上の pin プロパティのハンドラーを指定するオプションがありますが、これらのプロパティを認識しているクライアントだけがプロパティ要求を送信できます。

トポロジポートドライバーを除き、Portcls のすべてのポートドライバーは、次の pin プロパティの組み込みハンドラーを提供します。

[**KSK プロパティ\_接続\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-state)

[**KSK プロパティ\_接続\_DATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-dataformat)

[**KSK プロパティ\_接続\_ALLOCATORFRAMING**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing)

[**KSK プロパティ\_STREAM\_アロケーター**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)

[**KSK プロパティ\_ストリーム\_MASTERCLOCK**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-masterclock)

[**KSK プロパティ\_オーディオ\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)

[**KSPROPERTY\_DRMAUDIOSTREAM\_CONTENTID**](https://docs.microsoft.com/previous-versions/ff537351(v=vs.85))

この一覧の一部のプロパティには、ミニポートドライバーからのハードウェアに依存する情報が必要です。 ポートドライバーは、これらのプロパティのいずれかの要求を含む IRP を受信すると、その IRP をミニポートドライバーに渡しません。 代わりに、ポートドライバーは要求自体を処理しますが、そのハンドラーはミニポートドライバーのエントリポイントを呼び出すことによって、必要な情報を取得します。 たとえば、ポートドライバーでは、KSK プロパティ\_オーディオ\_位置要求の独自のプロパティハンドラーが提供されます。 このハンドラーは、単にミニポートドライバーストリームの**GetPosition**メソッド (たとえば、 [**IMiniportWavePciStream:: GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)) を呼び出して、現在の位置を取得します。

### <a name="span-idnode_propertiesspanspan-idnode_propertiesspanspan-idnode_propertiesspannode-properties"></a><span id="Node_Properties"></span><span id="node_properties"></span><span id="NODE_PROPERTIES"></span>ノードのプロパティ

ポートドライバーは、PCFILTER\_記述子の**Nodes**メンバーを介して、ミニポートドライバーのノードプロパティハンドラーにアクセスします。 このメンバーはノード記述子の配列を指し、各記述子はノード型のオートメーションテーブルを指します (ノード ID によって識別されます。これは単なる配列インデックスです)。 通常、ミニポートドライバーに属するすべてまたはほとんどのプロパティハンドラーは、 **Nodes**配列に存在します。 オーディオドライバーは、オーディオデバイス内のハードウェア制御をトポロジノードとして表し、プロパティメカニズムを使用して、ハードウェアに依存する制御設定へのアクセスをクライアントに提供します。

前述のように、クライアントはフィルタープロパティ要求をフィルターハンドルに送信し、ピンプロパティ要求をピンハンドルに送信します。 フィルターや pin のインスタンスとは異なり、ノードはカーネルオブジェクトではなく、ハンドルを持ちません。 クライアントは、ノードプロパティ要求をピンハンドルまたはフィルターハンドルのいずれかに送信しますが、要求では、要求がピンまたはフィルタープロパティではなくノードプロパティに対するものであることを示すノード ID も指定します。

次に、ノードプロパティがフィルターハンドルとピンハンドルのどちらを使用する必要があるかを判断するための一般的な規則を示します。

-   フィルターに特定のピンの種類のインスタンスが複数含まれており、その種類の各ピンに特定のノード ID を持つノードが含まれている場合、各ピンインスタンスにはノードのインスタンスが含まれます。 この場合、ノードプロパティ要求では、同じノード型の複数のインスタンスを区別するために、(フィルターハンドルだけではなく) ピンハンドルを指定する必要があります。 ピンハンドルとノード ID の組み合わせによって、特定のノードインスタンスが要求のターゲットとして明確に識別されます。

-   フィルターに特定のノードのインスタンスが1つしか含まれていない場合、ノードプロパティ要求ではフィルターハンドルが指定されます。 フィルターハンドルとノード ID を組み合わせるだけで、要求の対象となるノードを明確に識別できます。

ただし、特定のノードプロパティのハンドラーを実装する前に、ドライバーライターは、プロパティのターゲットをフィルターハンドルまたはピンハンドルとして指定する必要があるかどうかを確認するために、[オーディオドライバーのプロパティセット](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)を参照する必要があります。

現在、Portcls 内のポートドライバーは、ノードプロパティの組み込み処理を提供していません。ただし、KSK プロパティ\_トポロジ\_名は例外です。

### <a name="span-idoverspecified_and_underspecified_property_requestsspanspan-idoverspecified_and_underspecified_property_requestsspanspan-idoverspecified_and_underspecified_property_requestsspanoverspecified-and-underspecified-property-requests"></a><span id="Overspecified_and_Underspecified_Property_Requests"></span><span id="overspecified_and_underspecified_property_requests"></span><span id="OVERSPECIFIED_AND_UNDERSPECIFIED_PROPERTY_REQUESTS"></span>過剰に指定され、指定されたプロパティ要求が過剰である

ドライバーは、上記の規則に従っていないクライアントからのプロパティ要求を処理できるように準備する必要があります。 要求は、過剰に指定することも、指定しないこともできます。

-   **過剰指定の要求**

    プロパティ要求にフィルターハンドルのみが必要であっても、クライアントが pin ハンドルに要求を送信する場合、要求のターゲットは過剰に指定されます。 ただし、ドライバーは通常、要求を有効として扱います。つまり、pin を含むフィルターに送信された場合と同じように要求を処理します。

-   **指定された要求の過小処理**

    プロパティ要求にピンハンドルが必要であっても、クライアントがフィルターハンドルに要求を送信する場合は、要求のターゲットが指定されていません。 たとえば、フィルターに同じノード型の複数の pin インスタンスが含まれており、クライアントがそのノード型のプロパティの要求をピンハンドルではなくフィルターハンドルに送信した場合、ドライバーは、どのノードインスタンスが要求を受信する必要があるかを判断する方法がありません。 この場合、動作はドライバーによって異なります。 一部のドライバーでは、指定されたすべての要求が自動的に失敗するのではなく、指定されたセットのプロパティ要求が有効として扱われます。 この場合、この解釈は、要求によって指定されたノード ID の既定値が設定されることを意味します。 Pin ファクトリによって新しいノードインスタンスが作成されると、新しいノードに属するプロパティは既定値に初期化されます。 既定値を変更する要求は、要求の前に作成されたノードインスタンスには影響しません。 さらに、ドライバーは、プロパティに対してクエリを実行するノードインスタンスを決定する手段がないため、指定された get プロパティの要求が一様に失敗します。

### <a name="span-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>ルールの例外

歴史的な理由から、いくつかのオーディオプロパティには、これらの一般的な規則に違反する動作の特性があります。 次に例を示します。

-   「スピーカーの[構成設定の適用](applying-speaker-configuration-settings.md)」で説明されているように、クライアントは、3d ノード (KSNODETYPE) の[ **\_audio\_CHANNEL\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)プロパティを設定することによって、オーディオデバイスのスピーカー構成を変更でき[ **\_3D\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects))。 スピーカーの構成設定は、デバイスがスピーカーを介して再生するミックスの一部であるすべてのストリームのスピーカー構成を変更するため、グローバルです。 一般的な規則に従って、フィルター全体に影響を与えるノードプロパティ要求では、フィルターハンドル (およびノード ID) を指定する必要があります。 ただし、この特定のプロパティには、フィルターハンドルではなくピンハンドルが必要です。 ピンハンドルは、要求のターゲットである3d ノードを含む pin インスタンスを指定します。

-   [**Ksk プロパティ\_シンセサイザー\_ボリューム**](https://docs.microsoft.com/previous-versions/ff537409(v=vs.85))と[**KSK プロパティ\_シンセ\_masterclock**](https://docs.microsoft.com/previous-versions/ff537403(v=vs.85))は、シンセノード ([**KSNODETYPE\_シンセサイザー**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)) のプロパティです。 どちらもノードプロパティですが、これらのプロパティの要求にはノード Id は含まれません。 (要求のプロパティ記述子は、 [**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)ではなく、 [**ksproperty**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))型の構造体であることに注意してください)。この動作は、ノードプロパティがノード ID を必要とする一般的な規則に違反します。 この違いにかかわらず、いずれかのプロパティをサポートするミニポートドライバーでは、プロパティハンドラーが PCFILTER FILTER の**ノード**メンバー (**ピン**メンバーではなく) によって提供される必要があります。

 

 




