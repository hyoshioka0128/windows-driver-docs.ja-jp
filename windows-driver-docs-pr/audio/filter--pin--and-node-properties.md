---
title: フィルター、ピン、ノードのプロパティ
description: フィルター、ピン、ノードのプロパティ
ms.assetid: e0d52e97-459f-4095-9cf5-1474117ce66a
keywords:
- WDK、フィルターのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、フィルター
- WDK、ピンのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、ピン
- WDK、ノードのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、ノード
- フィルター プロパティ WDK オーディオ
- ノードのプロパティの WDK オーディオ
- KS フィルター WDK オーディオ、プロパティの要求
- プロパティ要求 WDK のオーディオをフィルター処理します。
- WDK のオーディオ、プロパティの概要をフィルター処理します。
- ノード WDK のオーディオ、プロパティの概要
- ピン WDK のオーディオ、プロパティの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a6075e54ad8626156e6c0efa43e57410533f702
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360030"
---
# <a name="filter-pin-and-node-properties"></a>フィルター、ピン、ノードのプロパティ


## <span id="filter_pin_and_node_properties"></span><span id="FILTER_PIN_AND_NODE_PROPERTIES"></span>


Microsoft Windows Driver Model (WDM) オーディオ ドライバー、KS フィルターとしてオーディオ デバイスを表すされ、フィルターで pin としてデバイスのハードウェアのバッファーを表します。 クライアントは、これらのフィルターまたは pin オブジェクトのいずれかにプロパティ要求を送信するポートのドライバーが要求を受信し、ポート ドライバーまたはミニポート ドライバーで適切なプロパティのハンドラーに要求をルーティングします。

オーディオ デバイスは、次の 3 つの種類のプロパティをサポートします。

-   **フィルターのプロパティ**

    フィルター プロパティは、特定の pin またはフィルター内のノードのプロパティではなく、全体として、フィルターのプロパティです。 要求フィルターのプロパティのフィルターのハンドルを指定するが、ノード Id を指定しないでください。

-   **Pin のプロパティ**

    暗証番号 (pin) のプロパティは、フィルターをピン留めする特定のインスタンスのプロパティです。 これらのプロパティに対する要求は、暗証番号 (pin) のハンドルを指定しますが、ノード Id を指定しないでください。

-   **ノードのプロパティ**

    ノードのプロパティは、フィルター内でそのトポロジ ノードのプロパティです。 ノード プロパティに関する要求は、フィルターのハンドルまたは暗証番号 (pin) のハンドルとノードの ID を指定します。

ノード プロパティの要求フィルターを指定するか、暗証番号 (pin) のハンドルは、ノードがフィルターに一意かどうかによって異なります。 詳細については、次のノードのプロパティ セクションを参照してください。

これら 3 つの要求のプロパティを次に示します: (インスタンスではフィルターまたは pin)、ノードにノード プロパティの要求が送信される、暗証番号 (pin) のインスタンスに送信される pin プロパティ要求、およびフィルター インスタンスに送信フィルター プロパティ要求。

![要求のフィルター、暗証番号 (pin)、およびノード プロパティを示す図](images/propreqs.png)

通常、ポート ドライバーは、フィルターおよび pin プロパティのほとんどの要求を処理し、ミニポート ドライバーがノードのプロパティに対する要求を処理します。

ポート ドライバーによって使用されるフィルターと pin のプロパティの独自の組み込みのハンドラーを提供する、 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver) (を参照してください[KSPROPSETID\_Sysaudio](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-sysaudio)と[KSPROPSETID\_Sysaudio\_Pin](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-sysaudio-pin)) と[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)します。 ミニポート ドライバーは、ポート ドライバーを処理するプロパティのハンドラーを実装する必要はありません。 一般的なミニポート ドライバーでは、フィルターと pin のプロパティの場合は、いくつかのハンドラーを提供します。 ミニポート ドライバーには、オーディオ デバイスのハードウェアに依存する機能を表すノードのプロパティのハンドラーが用意されています。 ポート ドライバー指定しない場合は、ノードのプロパティの組み込みの処理は例外です[ **KSPROPERTY\_トポロジ\_名前**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-name)します。

ポート ドライバーとミニポート ドライバーの両方が同じプロパティのハンドラーを指定時にポート ドライバーは、独自のハンドラーを使用して、ミニポート ドライバーのハンドラーは無視されます。

### <a name="span-idfilterdescriptorsspanspan-idfilterdescriptorsspanspan-idfilterdescriptorsspanfilter-descriptors"></a><span id="Filter_Descriptors"></span><span id="filter_descriptors"></span><span id="FILTER_DESCRIPTORS"></span>フィルター記述子

ポート ドライバーは、呼び出すことによって、ミニポート ドライバーのプロパティのハンドラーへのポインターを取得、 [ **IMiniport::GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)メソッド。 このメソッドでは、ポート ドライバーが型の構造体である、ミニポート ドライバーのフィルター記述子へのポインターを取得[ **PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)します。 この構造体は、フィルター、pin、およびノードのプロパティのミニポート ドライバーのプロパティのハンドラーを指定します。

-   PCFILTER\_記述子構造体の**AutomationTable**メンバーがフィルターのオートメーションのテーブルをポイントします。 このテーブルには、フィルターのプロパティのミニポート ドライバーのプロパティのハンドラーを指定します。

-   PCFILTER\_記述子構造体の**ピン**メンバーには、ピンのオートメーションのテーブルが含まれています。 各テーブルには、特定のピンの型の pin のプロパティのプロパティのハンドラーを指定します。

-   PCFILTER\_記述子構造体の**ノード**メンバーにはフィルター内のトポロジ ノードのオートメーションのテーブルが含まれています。 各テーブルには、特定のノード タイプのノード プロパティのプロパティのハンドラーを指定します。

### <a name="span-idfilterpropertiesspanspan-idfilterpropertiesspanspan-idfilterpropertiesspanfilter-properties"></a><span id="Filter_Properties"></span><span id="filter_properties"></span><span id="FILTER_PROPERTIES"></span>フィルターのプロパティ

ポート ドライバーを通じて、ミニポート ドライバーのフィルター プロパティ ハンドラーにアクセスする、 **AutomationTable** PCFILTER のメンバー\_記述子。 通常、この automation テーブルには、ポート ドライバーには、独自の組み込みハンドラー SysAudio と WDMAud クエリし、オーディオ デバイスの構成に使用するすべてのフィルター プロパティが用意されているためにほとんどのハンドラーが含まれません。

ただし、ミニポート ドライバーできますなどの指定のフィルター プロパティ ハンドラー [ **KSPROPERTY\_全般\_COMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-general-componentid)ハードウェア依存の情報を提供します。ポートのドライバーを利用でないです。 2 つのサンプル オーディオ ドライバー Microsoft Windows Driver Kit (WDK) での処理、KSPROPERTY\_全般\_COMPONENTID プロパティ。 詳細については、ミニポート ドライバーの実装、Msvad および Sb16 のサンプルを参照してください。

Portcls.sys にあるすべてのポート ドライバーの処理を提供する、 [KSPROPSETID\_Pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)と[KSPROPSETID\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)プロパティを設定します。 これらのセット内のすべてのプロパティは例外です、フィルタのプロパティを[ **KSPROPERTY\_トポロジ\_名前**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-name)、(pin ではない、フィルターのハンドルを使用しているノードのプロパティですハンドル、要求のターゲットを指定)。 ポート ドライバー、KSPROPSETID の次のサブセットをサポートする\_Pin のプロパティ。

[**KSPROPERTY\_PIN\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-category)

[**KSPROPERTY\_PIN\_CINSTANCES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-cinstances)

[**KSPROPERTY\_PIN\_通信**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-communication)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)

[**KSPROPERTY\_PIN\_CTYPES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-ctypes)

[**KSPROPERTY\_PIN\_データ フロー**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataflow)

[**KSPROPERTY\_PIN\_DATAINTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)

[**KSPROPERTY\_PIN\_DATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)

[**KSPROPERTY\_PIN\_GLOBALCINSTANCES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-globalcinstances)

[**KSPROPERTY\_PIN\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-interfaces)

[**KSPROPERTY\_PIN\_メディア**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-mediums)

[**KSPROPERTY\_PIN\_名**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-name)

[**KSPROPERTY\_PIN\_NECESSARYINSTANCES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-necessaryinstances)

[**KSPROPERTY\_PIN\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat2)

これらのプロパティは、フィルターに属する pin ファクトリに関する情報を提供します。 通常、クライアントは、暗証番号 (pin) のインスタンスを作成する前にこれらのプロパティ フィルターを照会します。 ポートのドライバー サポート、KSPROPSETID の 4 つすべて\_トポロジ プロパティは、フィルターの内部のトポロジに関する情報を提供します。

さらに、Dmu ポート ドライバーは、ハンドラーを[ **KSPROPERTY\_シンセサイザー\_MASTERCLOCK** ](https://docs.microsoft.com/previous-versions/ff537403(v=vs.85)) DirectMusic フィルターの取得専用プロパティであるプロパティ。 KSPROPERTY\_シンセサイザー\_MASTERCLOCK のメンバーである、 [KSPROPSETID\_SynthClock](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synthclock)プロパティ セット。

### <a name="span-idpinpropertiesspanspan-idpinpropertiesspanspan-idpinpropertiesspanpin-properties"></a><span id="Pin_Properties"></span><span id="pin_properties"></span><span id="PIN_PROPERTIES"></span>Pin のプロパティ

ポート ドライバーを通じて、ミニポート ドライバーの暗証番号 (pin) プロパティのハンドラーにアクセスする、**ピン**PCFILTER のメンバー\_記述子。 このメンバーが暗証番号 (pin) の記述子の配列をポイントし、各記述子がピン留めする型 (配列のインデックスでは単に、暗証番号 (pin) の ID によって識別される) の automation テーブルをポイントします。

通常、これらのオートメーション テーブルには、ポート ドライバー SysAudio と WDMAud を使用するすべての pin のプロパティの独自のハンドラーを提供するためにほとんどのエントリが含まれません。 ミニポート ドライバーがポート ドライバーが処理しない場合は、1 つまたは複数の pin のプロパティのハンドラーを指定できますが、これらのプロパティを認識するクライアントだけがそれらのプロパティの要求を送信できます。

を除き、トポロジ ポート ドライバーは、Portcls.sys にあるすべてのポート ドライバーは、pin のプロパティを次の組み込みのハンドラーを指定します。

[**KSPROPERTY\_接続\_状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-state)

[**KSPROPERTY\_接続\_DATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-dataformat)

[**KSPROPERTY\_接続\_ALLOCATORFRAMING**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-allocatorframing)

[**KSPROPERTY\_ストリーム\_アロケーター**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-allocator)

[**KSPROPERTY\_ストリーム\_MASTERCLOCK**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-masterclock)

[**KSPROPERTY\_オーディオ\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)

[**KSPROPERTY\_DRMAUDIOSTREAM\_CONTENTID**](https://docs.microsoft.com/previous-versions/ff537351(v=vs.85))

この一覧のプロパティの一部には、ミニポート ドライバーからハードウェアに依存する情報が必要です。 ポート ドライバーでは、これらのプロパティの 1 つの要求を含む IRP を受信するは IRP に渡さないミニポート ドライバー。 代わりに、ポート、ドライバー自体には、要求を処理するが、そのハンドラーは、ミニポート ドライバーでエントリ ポイントを呼び出すことによって必要な情報を取得します。 ポート ドライバーが KSPROPERTY の独自のプロパティのハンドラーを提供するなど、\_オーディオ\_位置要求。 このハンドラーには、ミニポート ドライバー ストリームの呼び出すだけです**GetPosition**メソッド (たとえば、 [ **IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)) 現在の位置を取得します。

### <a name="span-idnodepropertiesspanspan-idnodepropertiesspanspan-idnodepropertiesspannode-properties"></a><span id="Node_Properties"></span><span id="node_properties"></span><span id="NODE_PROPERTIES"></span>ノードのプロパティ

ポート ドライバーを通じて、ミニポート ドライバーのノード プロパティのハンドラーにアクセスする、**ノード**PCFILTER のメンバー\_記述子。 このメンバーがノードの記述子の配列をポイントし、各記述子が (配列のインデックスだけですが、ノードの ID によって識別される)、ノード タイプに対して automation テーブルをポイントします。 ミニポート ドライバーに属するプロパティ ハンドラーのほとんどすべてが存在する、通常、**ノード**配列。 オーディオ ドライバーはトポロジのノードとして、オーディオ デバイスでハードウェアの制御を表し、プロパティのメカニズムを使用して、ハードウェア依存の制御の設定にアクセス権を持つクライアントを提供します。

前述のように、クライアントは、および pin ハンドルにピン留めするプロパティの要求のフィルター処理に filter プロパティ要求を送信します。 フィルターまたは暗証番号 (pin) のインスタンスとは異なりノードは、カーネル オブジェクトではないと、ハンドルはありません。 クライアントは、暗証番号 (pin) のハンドルまたはフィルターのハンドルのいずれかにノード プロパティの要求を送信しますが、要求では、pin またはフィルターのプロパティではなく、ノードのプロパティの要求であることを示すノードの ID も指定します。

以下は、ノードのプロパティがフィルターのハンドルを使用する必要があるかどうか、またはハンドルをピン留めかどうかを決定するための一般的な規則です。

-   フィルターには、特定のピンの型の複数のインスタンスが含まれています。 その型の各ピンには、特定のノード ID を持つノードが含まれています。 場合は、各ピンのインスタンスにはによって、ノードのインスタンスが含まれます。 この場合、ノード プロパティ要求する必要があります暗証番号 (pin) のハンドル (なく指定フィルター ハンドルだけ) 同じノード型の複数のインスタンスを区別するためにします。 暗証番号 (pin) のハンドルとノードの ID の組み合わせは、要求のターゲットとして明確に特定のノード インスタンスを識別します。

-   フィルターに特定のノードの 1 つだけのインスタンスが含まれている場合、ノード プロパティの要求はフィルターのハンドルを指定します。 フィルターのハンドルとノードの ID の組み合わせは、要求の対象となっているノードを明確に識別するために十分です。

特定のノード プロパティのハンドラーを実装する前に、ドライバーのライターを参照してください[オーディオ ドライバーのプロパティ セット](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)ハンドルまたは暗証番号 (pin) が処理をフィルターとして、プロパティのターゲットを指定する必要があるかどうかを確認します。

Portcls.sys でポートのドライバーは、現在は KSPROPERTY を除く、ノードのプロパティの組み込みの処理を指定しない\_トポロジ\_名。

### <a name="span-idoverspecifiedandunderspecifiedpropertyrequestsspanspan-idoverspecifiedandunderspecifiedpropertyrequestsspanspan-idoverspecifiedandunderspecifiedpropertyrequestsspanoverspecified-and-underspecified-property-requests"></a><span id="Overspecified_and_Underspecified_Property_Requests"></span><span id="overspecified_and_underspecified_property_requests"></span><span id="OVERSPECIFIED_AND_UNDERSPECIFIED_PROPERTY_REQUESTS"></span>Overspecified し、プロパティの要求の仕様

ドライバーを準備して、上記の規則に従っていないクライアントからのプロパティの要求に対処する必要があります。 要求はありますか、overspecified または仕様します。

-   **Overspecified 要求**

    プロパティの要求が、フィルターのハンドルのみが必要ですが、クライアント要求を送信、暗証番号 (pin) のハンドルを代わりに、要求のターゲットが overspecified します。 ただし、ドライバー通常要求として扱う無効です。これは、要求として扱う、暗証番号 (pin) を格納しているフィルターに送信されたこと。

-   **選ば要求**

    プロパティの要求には、暗証番号 (pin) のハンドルが必要ですが、クライアントに要求を送信フィルターのハンドルを代わりに場合、要求のターゲットの仕様です。 たとえば、フィルターには、同じノードの種類をいくつかの暗証番号 (pin) インスタンスと、クライアントは、暗証番号 (pin) のハンドルではなく、フィルターのハンドルにそのノード型のプロパティの要求を送信、ドライバーがありませんノード インスタンスが要求を受信する必要がありますを決定する方法。 この場合、動作は、ドライバーによって異なります。 自動的に選ばのすべての要求が失敗するのではなくは、一部のドライバーは、有効なとして選ばのプロパティの設定要求を処理します。 ここでは、解釈は、要求が指定したノード ID の既定値を設定します。 暗証番号 (pin) ファクトリは、ノードの新しいインスタンスを作成するときは、新しいノードに属するプロパティが既定値に初期化されます。 既定値を変更する要求は、要求の前に作成されたノードのインスタンスへの影響を与えません。 さらに、ドライバーでは一様に選ばプロパティ get 要求を失敗して、ハンドラーは、プロパティを照会するには、どのノード インスタンスを特定する方法があるないためです。

### <a name="span-idexceptionstotherulesspanspan-idexceptionstotherulesspanspan-idexceptionstotherulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>ルールの例外

歴史的な理由から、オーディオ、いくつかのプロパティはこれらの一般的な規則に違反している行動 quirks があります。 次に例を示します。

-   」の説明に従って[スピーカー構成設定の適用](applying-speaker-configuration-settings.md)、クライアントは設定してスピーカーのオーディオ デバイスの構成を変更することができます、 [ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config) 3-D ノードのプロパティ ([**KSNODETYPE\_3D\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects))。 デバイスは、スピーカーから再生をミックスに含まれるすべてのストリームのスピーカーの構成を変更するため、スピーカーの構成設定はグローバルです。 フィルター全体に影響を与えるノード プロパティの要求には、一般的な規則に従って、フィルター ハンドル (とノード ID) を指定する必要があります。 ただし、この特定のプロパティには、フィルターのハンドルではなく暗証番号 (pin) のハンドルが必要です。 暗証番号 (pin) のハンドルは、要求の対象となっている 3-D ノードを含む暗証番号 (pin) のインスタンスを指定します。

-   [**KSPROPERTY\_シンセサイザー\_ボリューム**](https://docs.microsoft.com/previous-versions/ff537409(v=vs.85))と[ **KSPROPERTY\_シンセサイザー\_MASTERCLOCK** ](https://docs.microsoft.com/previous-versions/ff537403(v=vs.85))のプロパティは、シンセサイザー ノード ([**KSNODETYPE\_シンセサイザー**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer))。 ノードのプロパティは両方が、これらのプロパティに対する要求はノード Id は含まれません。 (型の構造体は、要求のプロパティ記述子、 [ **KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))ではなく、 [ **KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty))。この動作ノードのプロパティが、ノード ID が必要である一般的な規則に違反しています このような相違に関係なく、これらのプロパティをサポートしているミニポート ドライバーを使用して、プロパティ ハンドラーを指定します、**ノード**PCFILTER のメンバー\_記述子 (の代わりに、**ピン**。メンバーの場合)。

 

 




