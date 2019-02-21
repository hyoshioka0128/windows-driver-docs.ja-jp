---
title: Jack の Description プロパティ
description: Jack の Description プロパティ
ms.assetid: 6398efc9-4435-4234-bd72-1ed0f96c9f9f
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8f579dab6541c820f0cc1af2be276b4801c2cd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539370"
---
# <a name="jack-description-property"></a>Jack の Description プロパティ


Windows Vista 以降では、 [ **KSPROPERTY\_ジャック\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)プロパティがオーディオのアダプターでのオーディオ ジャックまたはその他の物理的なコネクタをについて説明します。 プロパティの値には、回線のモジュラー ジャックの色、ジャック、コネクタの種類、およびその他の回線のモジュラー ジャック機能の物理的な場所について説明します。 この情報の目的は、マイク、ヘッドホン、スピーカーなど、エンドポイントのオーディオ デバイスを接続するための正しいジャックを検索するユーザーを支援します。 詳細については、次を参照してください。[オーディオ エンドポイント デバイス](https://go.microsoft.com/fwlink/p/?linkid=130876)します。

オーディオのアダプターで KS フィルターが、KSPROPERTY をサポートしているか\_ジャック\_DESCRIPTION プロパティ、フィルターにピン留め、ブリッジのジャック情報、Windows マルチ メディア コントロール パネル、Mmsys.cpl、表示します。 ブリッジ暗証番号 (pin) は、エンドポイントのオーディオ デバイスへの接続を (通常、ジャック) を表します。 プロパティの値には、pin (または代わりに、回線のモジュラー ジャックまたはジャック、暗証番号 (pin) に関連付けられている) に関する情報が含まれますが、プロパティ、プロパティのフィルターではなく、暗証番号 (pin) です。 ブリッジの pin の詳細については、次を参照してください。[オーディオ フィルター グラフ](audio-filter-graphs.md)します。 フィルターのプロパティと pin のプロパティの詳細については、次を参照してください。[フィルター、Pin、およびノードのプロパティ](filter--pin--and-node-properties.md)します。

オーディオのアプリケーションは、KSPROPERTY を取得できます\_ジャック\_呼び出すことによって、エンドポイントのオーディオ デバイスの説明プロパティの値、 **IKsJackDescription::GetJackDescription** DeviceTopology メソッドAPI です。 たとえば、アプリケーションでは、オレンジ色の XLR ジャックに接続されているマイクから緑 XLR ジャックに接続したマイクを区別するためにユーザーを支援するのにジャック情報を使用できます。 DeviceTopology API の詳細については、次を参照してください。[デバイス トポロジ](https://go.microsoft.com/fwlink/p/?linkid=130878)します。

Microsoft HD オーディオ クラス ドライバーによって自動的に構築、KSPROPERTY\_ジャック\_HD オーディオ コーデックでピン構成のレジスタから読み取ったデータからプロパティ値を説明します。 ただし、KS ベースとするオーディオ ドライバー、フィルターのオートメーション テーブルで、このプロパティのサポートを実装できます。 HD オーディオ クラス ドライバーの詳細については、次を参照してください。 [HD オーディオおよび UAA](hd-audio-and-uaa.md)します。 レジスタの暗証番号 (pin) 構成の詳細については、次を参照してください。[高定義オーディオ デバイスの暗証番号 (pin) の構成ガイドライン](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PinConfig.doc)ホワイト ペーパー。

エンドポイントのオーディオ デバイスは、1 つまたは複数のジャックからブリッジのピンに接続できます。 たとえば、ステレオのスピーカーの (2 つのチャネル) のセットが 1 つのジャックが必要ですが、5.1 サラウンド サウンドのスピーカーのセットは、(各ジャックが 2 つの 6 つのチャネルを処理) すると仮定すると 3 つのジャックが必要です。

各ジャックの説明が含まれている、 [ **KSJACK\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)構造体。 KSPROPERTY など\_ジャック\_DESCRIPTION プロパティの値 1 つのジャックが付いたオーディオ エンドポイント デバイスにはには、1 つ KSJACK が含まれています\_説明構造体が 3 つのジャックとデバイスのエンドポイント プロパティの値。次の 3 つ KSJACK が含まれています\_構造を説明します。 どちらの場合、KSJACK\_構造を定義またはプロパティの値構造体の前は、 [ **KSMULTIPLE\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff563441)構造体のサイズを指定する、プロパティ値です。 詳細については、次を参照してください。 [ **KSPROPERTY\_ジャック\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)します。

回線のモジュラー ジャック情報は、マルチ チャネルのスピーカーの構成に接続するジャックを区別するために特に便利です。 次のコード例は、KSJACK の配列を示しています。\_オーディオ ドライバーを使用して、5.1 サラウンド スピーカー一連の 3 つのジャックを記述する構造を説明します。

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

オーディオ ハードウェア、デバイスが接続されているかどうかを検出できる場合、ドライバーを動的に更新、デバイスが現在接続されているかどうかを示すには、このメンバーの値 (**TRUE**) または電源が入っていない (**FALSE**)

上記のコード例で、 **IsConnected**に配列の各要素内のメンバーが設定されている**TRUE**エンドポイント デバイスがジャックに接続されていることを示す。 ただし、ハードウェア ジャック プレゼンスがない場合の検出、 **IsConnected**に常に設定する必要があります**TRUE**ジャックに接続されているデバイスがあるかどうか。 この 2 つの意味に起因するあいまいさを削除する、 **TRUE**戻り値は、クライアント アプリケーションが呼び出すことができます[IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)の JackCapabilities フラグを読み取る[ **KSJACK\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537138)構造体。 このフラグは、JACKDESC2 場合\_プレゼンス\_検出\_機能ビットが設定、エンドポイントは実際にはジャック プレゼンスの検出にサポートを示します。 その場合の値、 **IsConnected**メンバーは、ジャックのカーソルの状態を正確に反映として解釈できます。

上記の構造で表示される RGB マクロは、ヘッダー ファイル、Windows sdk Wingdi.h で定義されます。

さらの 2 つ以上のジャックが機能的には他の回線のモジュラー ジャックの説明の配列を使用できます。 次のコード例では、オーディオ ドライバーは、2 つのジャックが同じ信号を実行するユーザーに示すために 1 つの配列にジャック説明、黄色の RCA ジャックと黒のデジタル光学ジャックを結合します。

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

上記のコード例の値で、 **ChannelMapping** KSJACK を 2 つのメンバー\_説明構造は同じです。

「簡単」MSVAD サンプル ドライバー WDK に含まれて (サンプル ディレクトリ Src\\オーディオ\\Msvad\\単純な)、KSPROPERTY をサポートするために採用できる\_ジャック\_DESCRIPTION プロパティ。 このサンプル ドライバーは、実際のハードウェアが必要がないため、プロパティの使用方法を示すために便利です。 したがって、Windows を実行するコンピューターでインストールできます。 (ただし、Windows Vista およびそれ以降のオペレーティング システム、KSPROPERTY の完全なサポートを提供するだけ\_ジャック\_DESCRIPTION プロパティ)。このサンプルの詳細については、次を参照してください。 [Windows ドライバー キット サンプル](https://msdn.microsoft.com/library/windows/hardware/ff554118)します。

用の単純な MSVAD サンプル トポロジ フィルターは、次の 3 つのブリッジのピンを定義します。 これらのピンは、次の表に一覧表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">暗証番号 (pin) の ID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPIN_TOPO_SYNTHIN_SOURCE</p></td>
<td align="left"><p>MIDI 入力ジャックに接続</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_TOPO_MIC_SOURCE</p></td>
<td align="left"><p>マイク入力ジャックに接続</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSPIN_TOPO_LINEOUT_DEST</p></td>
<td align="left"><p>ステレオのスピーカー出力ジャック</p></td>
</tr>
</tbody>
</table>

 

このトピックの残りの部分では、次の 3 つのブリッジのピンのジャック情報を提供する単純な MSVAD サンプル ドライバーを変更する方法について説明します。

最初に、次のように、これらのピンのジャック情報を指定できます。

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

上記のコード例のセット、 **ChannelMapping**メンバーを 0 に 2 つのキャプチャの pin を使用します。 アナログのみレンダリング ピンが 0 以外の場合必要**ChannelMapping**値。

MSVAD の単純なサンプルを基本的な変更では、Mintopo.cpp のサンプル ファイルでトポロジ ミニポートの実装に次のプロパティのハンドラーを追加します。

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

上記のコード例を次の 3 つの KSJACK 指す\_説明の変数 - SynthIn\_ジャック、MicIn\_ジャックとライン出力\_Jack - 以前に定義されています。 クエリが成功した場合は、クライアント ブリッジ pin ではありません (とジャックの説明を持たない) を有効な暗証番号 (pin)、1 つの回線のモジュラー ジャックの説明については、フィルター処理するクエリ、(状態コード状態\_成功)、プロパティ ハンドラーは、空のジャックを返しますが、説明、KSMULTIPLE から成る\_項目の構造とその他に何もします。 クライアントは、(存在しない暗証番号 (pin) を識別します) をピン留めする無効な ID を指定する場合、ハンドラーはステータス コードの状態を返します\_無効な\_パラメーター。

単純な MSVAD サンプルに 2 つの追加の変更が、KSPROPERTY をサポートするために必要な\_ジャック\_DESCRIPTION プロパティ。 それらを次に示します。

-   宣言を追加、 **PropertyHandlerJackDescription**ヘッダー ファイル Mintopo.h CMiniportTopology クラス定義には、上記のコード例のメソッド。

-   トポロジ フィルター テーブルをオートメーションを実装し、このテーブルのアドレスを読み込む、 **AutomationTable**のメンバー、 [ **PCFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537694)Toptable.h のヘッダー ファイルの構造体。 この構造体の名前は**MiniportFilterDescriptor**します。

Automation の表に、フィルターを実装するには、ヘッダー ファイル Toptable.h に次のコードを挿入 (の定義の前に**MiniportFilterDescriptor**)。

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

上記のコード例で、**ハンドラー**のメンバー、 [ **PCPROPERTY\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff537722)構造には、プロパティ ハンドラーへの関数ポインターが含まれています前の手順で Mintopo.cpp に追加されます。 プロパティ ハンドラーをヘッダー ファイルからアクセスできるようにするには挿入、 **extern**関数の宣言の PropertyHandler\_TopoFilter ヘッダー ファイルの先頭。

Jack の description プロパティの詳細については、次を参照してください。[動的オーディオ サブデバイスのジャック説明](jack-descriptions-for-dynamic-audio-subdevices.md)します。

 

 




