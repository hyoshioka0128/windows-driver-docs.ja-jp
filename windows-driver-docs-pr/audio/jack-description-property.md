---
title: ジャック説明のプロパティ
description: ジャック説明のプロパティ
ms.assetid: 6398efc9-4435-4234-bd72-1ed0f96c9f9f
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: dfea9a4cb1a229d997435ff597fc11d233117705
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833195"
---
# <a name="jack-description-property"></a>ジャック説明のプロパティ


Windows Vista 以降では、 [**Ksk プロパティ\_ジャック\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)プロパティは、オーディオアダプターまたはオーディオアダプター上のその他の物理コネクタを記述します。 プロパティ値は、ジャックの色、ジャックの物理的な位置、コネクタの種類、およびその他のジャック機能を表します。 この情報の目的は、マイク、ヘッドホン、スピーカーなどのオーディオエンドポイントデバイスに接続するための適切なジャックをユーザーが見つけることができるようにすることです。 詳細については、「[オーディオエンドポイントデバイス](https://go.microsoft.com/fwlink/p/?linkid=130876)」を参照してください。

オーディオアダプターの KS フィルターで、KSK プロパティ\_ジャック\_DESCRIPTION プロパティがサポートされている場合、Windows マルチメディアコントロールパネルである Mmsys が、フィルターのブリッジピンのジャック情報を表示します。 ブリッジ pin は、オーディオエンドポイントデバイスへの接続 (通常はジャック) を表します。 プロパティ値には、pin (または pin に関連付けられているジャック) に関する情報が含まれていますが、プロパティは、pin ではなく、フィルターのプロパティです。 ブリッジピンの詳細については、「[オーディオフィルターグラフ](audio-filter-graphs.md)」を参照してください。 フィルターのプロパティとピンのプロパティの詳細については、「[フィルター、ピン留め、およびノードのプロパティ](filter--pin--and-node-properties.md)」を参照してください。

オーディオアプリケーションでは、DeviceTopology API で**IKsJackDescription:: GetJackDescription**メソッドを呼び出すことによって、オーディオエンドポイントデバイスの ksk プロパティ\_ジャック\_DESCRIPTION プロパティ値を取得できます。 たとえば、アプリケーションでは、ジャック情報を使用して、オレンジ色の XLR ジャックに接続されているマイクから、緑色の XLR ジャックに接続されているマイクを区別することができます。 DeviceTopology API の詳細については、「[デバイストポロジ](https://go.microsoft.com/fwlink/p/?linkid=130878)」を参照してください。

Microsoft HD audio クラスドライバーは、HD オーディオコーデックのピン構成レジスタから読み取るデータから、KSK プロパティ\_JACK\_DESCRIPTION プロパティ値を自動的に構築します。 ただし、すべての KS ベースのオーディオドライバーは、フィルター自動化テーブルにこのプロパティのサポートを実装できます。 HD オーディオクラスドライバーの詳細については、「 [hd audio AND UAA](hd-audio-and-uaa.md)」を参照してください。 Pin 構成レジスタの詳細については、「[高解像度オーディオデバイス用の Pin 構成ガイドライン](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PinConfig.doc)」ホワイトペーパーを参照してください。

オーディオエンドポイントデバイスは、1つまたは複数のジャックを介してブリッジピンに接続できます。 たとえば、一連の (2 チャネル) ステレオスピーカーには1つのジャックが必要ですが、5.1 のサラウンドサウンドスピーカーのセットには3つのジャックが必要です (各ジャックが6チャネルのうち2つを処理することを前提としています)。

各ジャックの説明は、 [**Ksk ジャック\_description**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)構造体に含まれています。 たとえば、1つのジャックを持つオーディオエンドポイントデバイスの KSK プロパティ\_ジャック\_DESCRIPTION プロパティ値には、1つの KSK ジャック\_DESCRIPTION 構造体が含まれていますが、3つのジャックを持つエンドポイントデバイスのプロパティ値には3つの KSK ジャックが含まれています\_説明の構造体。 どちらの場合も、プロパティ値に含まれる KSK ジャック\_DESCRIPTION 構造体または構造体の前に、プロパティ値のサイズを指定する[**Ksjack\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)構造体が付きます。 詳細については、「 [**Ksk プロパティ\_ジャック\_の説明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)」を参照してください。

ジャック情報は、マルチチャンネルスピーカー構成に接続するジャックをユーザーが区別できるようにするために特に役立ちます。 次のコード例は、5.1 サラウンドスピーカーのセットの3つのジャックを説明するためにオーディオドライバーが使用する KSK ジャック\_記述構造体の配列を示しています。

```cpp
KSJACK_DESCRIPTION ar_5dot1_Jacks[] =
{
    // Jack 1
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // ChannelMapping (L,R)
        RGB(0,255,0),       // Color (green)
        eConnType3Point5mm, // ConnectionType
        eGeoLocRear,        // GeoLocation
        eGenLocPrimaryBox,  // GenLocation
        ePortConnJack,      // PortConnection
        TRUE                // IsConnected
    },
    // Jack 2
    {
        (SPEAKER_FRONT_CENTER | SPEAKER_LOW_FREQUENCY), // (C,Sub)
        RGB(0,0,255),       // (red)
        eConnType3Point5mm,
        eGeoLocRear,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    },
    // Jack 3
    {
        (SPEAKER_SIDE_LEFT | SPEAKER_SIDE_RIGHT),  // (SL,SR)
        RGB(0,255,255),     // (yellow)
        eConnType3Point5mm,
        eGeoLocRear,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};
```

オーディオハードウェアがデバイスが接続されているかどうかを検出できる場合、ドライバーはこのメンバーの値を動的に更新して、デバイスが現在接続されている (**TRUE**) か、または取り外されている (**FALSE**) かを示します。

前のコード例では、各配列要素の**IsConnected**メンバーは、エンドポイントデバイスがジャックに接続されていることを示すために**TRUE**に設定されています。 ただし、ハードウェアにジャックの存在が検出されない場合は、ジャックにデバイスが接続されているかどうかにかかわらず、 **IsConnected**を常に**TRUE**に設定する必要があります。 **真**の戻り値のこの2つの意味の結果として得られるあいまいさを解消するために、クライアントアプリケーションは[IKsJackDescription2:: GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)を呼び出して、 [**Ksjack\_DESCRIPTION2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description2)の JackCapabilities フラグを読み取ることができます。データ. このフラグによって\_機能ビットセット\_検出された場合は、エンドポイントが\_ジャックのプレゼンス検出をサポートしていることを示します。 その場合、 **IsConnected**メンバーの値は、ジャックの挿入状態を正確に反映したものとして解釈できます。

前の構造体に表示される RGB マクロは、Windows SDK のヘッダーファイルウィング Di で定義されています。

さらに、複数のジャックが機能的に同等であることを示すために、ジャック記述の配列を使用することもできます。 次のコード例では、オーディオドライバーが黄色の RCA ジャックのジャックの説明と黒のデジタル光学式のジャックを1つの配列に結合して、2つのジャックが同じ信号を持っていることをユーザーに示しています。

```cpp
KSJACK_DESCRIPTION ar_SPDIF_Jacks[] =
{
    // Jack 1
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // ChannelMapping (L,R)
        RGB(0,255,255),         // Color (yellow)
        eConnTypeRCA,           // ConnectionType (RCA)
        eGeoLocRear,            // GeoLocation
 eGenLocPrimaryBox,   // GenLocation
        ePortConnJack,       // PortConnection
        TRUE                    // IsConnected
    },
    // Jack 2
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // (L,R)
        RGB(0,0,0),             // (black)
        eConnTypeOptical,       // (optical)
        eGeoLocRear,
 eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};
```

前のコード例では、2つの KSK ジャック\_DESCRIPTION 構造体の**Channelmapping**メンバーの値は同一です。

WDK の "Simple" MSVAD サンプルドライバー (サンプルディレクトリ Src\\Audio\\Msvad\\Simple) は、KSK プロパティ\_ジャック\_DESCRIPTION プロパティをサポートするように調整できます。 このサンプルドライバーは、実際のハードウェアを必要としないため、プロパティの使用方法を示すのに便利です。 そのため、Windows を実行している任意のコンピューターにインストールできます。 (ただし、Windows Vista 以降のオペレーティングシステムでは、KSK プロパティ\_ジャック\_DESCRIPTION プロパティが完全にサポートされています)。このサンプルの詳細については、「 [Windows Driver Kit Samples](https://docs.microsoft.com/windows-hardware/drivers/samples/index)」を参照してください。

Simple MSVAD サンプルのトポロジフィルターでは、3つのブリッジピンが定義されています。 これらの pin を次の表に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Pin ID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPIN_TOPO_SYNTHIN_SOURCE</p></td>
<td align="left"><p>MIDI 入力ジャック</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_TOPO_MIC_SOURCE</p></td>
<td align="left"><p>マイク入力ジャック</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSPIN_TOPO_LINEOUT_DEST</p></td>
<td align="left"><p>ステレオスピーカーの出力ジャック</p></td>
</tr>
</tbody>
</table>

 

このトピックの残りの部分では、単純な MSVAD サンプルドライバーを変更して、3つのブリッジピンのジャック情報を提供する方法について説明します。

まず、これらの pin のジャック情報は、次のように指定できます。

```cpp
// Describe MIDI input jack (pin ID = KSPIN_TOPO_SYNTHIN_SOURCE).
static KSJACK_DESCRIPTION SynthIn_Jack[] =
{
    {
        0,                  // ChannelMapping
        RGB(255,255,0),    // Color (cyan)
 eConnType3Point5mm, // ConnectionType
        eGeoLocRear,        // GeoLocation
        eGenLocPrimaryBox,  // GenLocation
        ePortConnJack,      // PortConnection
        TRUE                // IsConnected
    }
};

// Describe microphone jack (pin ID = KSPIN_TOPO_MIC_SOURCE).
static KSJACK_DESCRIPTION MicIn_Jack[] =
{
    {
        0,
        RGB(0,128,255),   // (orange)
 eConnType3Point5mm,
        eGeoLocFront,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};

// Describe stereo speaker jack (pin ID = KSPIN_TOPO_LINEOUT_DEST).
static KSJACK_DESCRIPTION LineOut_Jack[] =
{
    {
        (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT), // ChannelMapping (L,R)
        RGB(0,255,0),       // (green)
 eConnType3Point5mm,
        eGeoLocRear,
        eGenLocPrimaryBox,
        ePortConnJack,
        TRUE
    }
};
```

上記のコード例では、2つのキャプチャピンの**Channelmapping**メンバーを0に設定しています。 アナログレンダリングピンのみが0以外の**Channelmapping**値を持つ必要があります。

単純な MSVAD サンプルの主な変更は、次のプロパティハンドラーをサンプルファイル Mintopo .cpp のトポロジミニポートの実装に追加することです。

```cpp
#define ARRAY_LEN(a)  sizeof(a)/sizeof(a[0]);
#define MAXIMUM_VALID_PIN_ID  KSPIN_TOPO_WAVEIN_DEST

NTSTATUS
CMiniportTopology::PropertyHandlerJackDescription(
               IN PPCPROPERTY_REQUEST PropertyRequest)
{
    PAGED_CODE();

    ASSERT(PropertyRequest);

    DPF_ENTER(("[PropertyHandlerJackDescription]"));

    NTSTATUS ntStatus = STATUS_INVALID_DEVICE_REQUEST;
    ULONG nPinId = (ULONG)-1;

    if (PropertyRequest->InstanceSize >= sizeof(ULONG))
    {
        nPinId = *((PULONG)(PropertyRequest->Instance));

        if (nPinId > MAXIMUM_VALID_PIN_ID)
        {
            ntStatus = STATUS_INVALID_PARAMETER;
        }
        else if (PropertyRequest->Verb & KSPROPERTY_TYPE_BASICSUPPORT)
        {
            ntStatus = PropertyHandler_BasicSupport(
                            PropertyRequest,
                            KSPROPERTY_TYPE_BASICSUPPORT | KSPROPERTY_TYPE_GET,
                            VT_ILLEGAL);
        }
        else
        {
            PKSJACK_DESCRIPTION pJack = NULL;
            ULONG cJacks = 0;

            switch (nPinId)
            {
            case KSPIN_TOPO_SYNTHIN_SOURCE:
                pJack = SynthIn_Jack;
                cJacks = ARRAY_LEN(SynthIn_Jack);
                break;
            case KSPIN_TOPO_MIC_SOURCE:
                pJack = MicIn_Jack;
                cJacks = ARRAY_LEN(MicIn_Jack);
                break;
            case KSPIN_TOPO_LINEOUT_DEST:
                pJack = LineOut_Jack;
                cJacks = ARRAY_LEN(LineOut_Jack);
                break;
            default:
                break;
            }

            ULONG cbNeeded = sizeof(KSMULTIPLE_ITEM) +
                             sizeof(KSJACK_DESCRIPTION) * cJacks;

            if (PropertyRequest->ValueSize == 0)
            {
                PropertyRequest->ValueSize = cbNeeded;
                ntStatus = STATUS_BUFFER_OVERFLOW;
            }
            else if (PropertyRequest->ValueSize < cbNeeded)
            {
                ntStatus = STATUS_BUFFER_TOO_SMALL;
            }
            else if (PropertyRequest->Verb & KSPROPERTY_TYPE_GET)
            {
                PKSMULTIPLE_ITEM pMI = (PKSMULTIPLE_ITEM)PropertyRequest->Value;

                pMI->Size = cbNeeded;
                pMI->Count = cJacks;

                // Copy jack description structure into Value buffer.
                // RtlCopyMemory correctly handles the case Length=0.
                PKSJACK_DESCRIPTION pDesc = (PKSJACK_DESCRIPTION)(pMI + 1);

                RtlCopyMemory(pDesc, pJack, pMI->Size * pMI->Count);

                ntStatus = STATUS_SUCCESS;
            }
        }
    }

    return ntStatus;
}

NTSTATUS
PropertyHandler_TopoFilter(IN PPCPROPERTY_REQUEST PropertyRequest)
{
    PAGED_CODE();

    ASSERT(PropertyRequest);

    DPF_ENTER(("[PropertyHandler_TopoFilter]"));

    // PropertyRequest structure is filled by PortCls.
    // MajorTarget is a pointer to miniport object for miniports.
    //
    NTSTATUS ntStatus = STATUS_INVALID_DEVICE_REQUEST;
    PCMiniportTopology pMiniport = (PCMiniportTopology)PropertyRequest->MajorTarget;

    if (IsEqualGUIDAligned(*PropertyRequest->PropertyItem->Set, KSPROPSETID_Jack) &&
        (PropertyRequest->PropertyItem->Id == KSPROPERTY_JACK_DESCRIPTION))
    {
        ntStatus = pMiniport->PropertyHandlerJackDescription(PropertyRequest);
    }

    return ntStatus;
}
```

前のコード例では、前に定義した3つの KSK ジャック\_説明変数-SynthIn\_ジャック、MicIn\_Jack、LineOut\_ジャックを参照しています。 クライアントは、有効な pin のジャックの説明に対してフィルターにクエリを実行しますが、1つはブリッジピンではなく (したがって、ジャックの説明がない)、クエリは成功しますが (状態コードの状態\_SUCCESS)、プロパティハンドラーは空のジャックの説明を返します。KSMULTIPLE\_ITEM 構造体で構成されます。 クライアントが無効な pin ID (存在しない pin を識別する) を指定した場合、ハンドラーはステータスコードの状態\_無効な\_パラメーターとして返します。

KSK プロパティ\_JACK\_DESCRIPTION プロパティをサポートするには、単純な MSVAD サンプルに対する2つの追加の変更が必要です。 それらを次に示します。

-   前のコード例の**PropertyHandlerJackDescription**メソッドの宣言を、ヘッダーファイル Mintopo .H の CMiniportTopology クラス定義に追加します。

-   トポロジフィルター用のオートメーションテーブルを実装し、このテーブルのアドレスを、ヘッダーファイル Toptable .h の[**pcfilter\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)構造体の**AutomationTable**メンバーに読み込みます。 この構造体の名前は**Miniportfilterdescriptor**です。

フィルターのオートメーションテーブルを実装するには、次のコードをヘッダーファイル Toptable .h ( **Miniportfilterdescriptor**の定義の前) に挿入します。

```cpp
static PCPROPERTY_ITEM PropertiesTopoFilter[] =
{
    {
        &KSPROPSETID_Jack,
        KSPROPERTY_JACK_DESCRIPTION,
        KSPROPERTY_TYPE_GET | KSPROPERTY_TYPE_BASICSUPPORT,
        PropertyHandler_TopoFilter
    }
};

DEFINE_PCAUTOMATION_TABLE_PROP(AutomationTopoFilter, PropertiesTopoFilter);
```

前のコード例では、 [**Pcproperty\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item)構造体の**ハンドラー**メンバーに、前の手順で mintopo .cpp に追加されたプロパティハンドラーへの関数ポインターが含まれています。 ヘッダーファイルからプロパティハンドラーにアクセスできるようにするには、ヘッダーファイルの先頭に PropertyHandler\_TopoFilter の**extern**関数宣言を挿入します。

"ジャックの説明" プロパティの詳細については、「[動的オーディオサブデバイスのジャックの説明](jack-descriptions-for-dynamic-audio-subdevices.md)」を参照してください。

 

 




