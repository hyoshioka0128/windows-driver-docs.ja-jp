---
title: トポロジのピン
description: トポロジのピン
ms.assetid: b434e2a7-4acc-4ef1-9db9-8f1b82f68de3
keywords:
- トポロジ pin WDK オーディオ
- WDK オーディオ、トポロジをピン留めする
- S/PDIF ピン翻訳 WDK オーディオ
- WDK オーディオをピン留めし、翻訳する
- KS WDK audio をピン留めし、翻訳する
- WDK オーディオ、記述子をピン留めする
- ミキサー-ライン記述子 WDK オーディオ
- ソースミキサーライン WDK オーディオ
- 宛先ミキサーの線 WDK オーディオ
- pin の変換 WDK オーディオ
- ファクトリ WDK オーディオをピン留めする
- PCPIN_DESCRIPTOR 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf5f99615cc377bfae1528448af03d16617681e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832333"
---
# <a name="topology-pins"></a>トポロジのピン


## <span id="topology_pins"></span><span id="TOPOLOGY_PINS"></span>


[WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)は、ミキサフィルターのトポロジピンを、ミキサー API がアプリケーションに公開するソースとターゲットのミキサ線に変換します。 入力 (シンク) ピンがソースミキサーの線になり、出力 (ソース) ピンがターゲットミキサーの線になります。

「 [Pin ファクトリ](pin-factories.md)」で説明されているように、ミニポートドライバーは、ピン記述子の配列を提供します。各記述子は、フィルターに属するピンファクトリを記述する[**PCPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)の構造体です。 各 pin 記述子には、次の情報が含まれています。

-   **データフロー方向指定子**

    データストリームを入力するか (KSPIN\_データフロー\_)、ピンを使用してフィルターを終了するか (KSPIN\_データフローを\_) を終了するかを示します。

-   **KS pin カテゴリ GUID**

    Pin が属しているピンカテゴリを示します。 たとえば、オーディオ再生デバイスでは、1つのピンが wave 形式のデジタルオーディオストリームを受け取ることがあり、別の pin がスピーカーを駆動するアナログオーディオ信号を生成する場合があります。 ミニポートドライバーでは、これらの2種類の pin が個別の pin カテゴリに属しているものとして識別されます。

-   **通信の種類指定子**

    Pin がサポートする IRP 通信の種類を示します。 Irp 通信をサポートする pin は、IRP シンク (KSPIN\_通信\_シンク)、IRP ソース (KSPIN\_通信\_ソース)、またはその両方 (KSPIN\_通信\_両方) にすることができます。 IRP 通信をサポートしていない pin は、KS フィルターグラフ (KSPIN\_通信\_なし) の内側に配置することも、グラフのエンドポイント (KSPIN\_通信\_ブリッジ) の*ブリッジ pin*にすることもできます。

ブリッジピンの詳細については、「[オーディオフィルターグラフ](audio-filter-graphs.md)」を参照してください。

WDMAud は、ミニポートドライバーの pin 記述子の情報を、次の情報を含む MIXERLINE 型の構造であるミキサーライン記述子に変換します。

-   **ミキサー-線コンポーネントの種類**

    ミキサーの線が変換元または変換先の行であるかどうかを示します。また、ミキサーの線の一般的な機能も示します。 たとえば、wave 出力 (レンダリング) ストリームから生成されたアナログ信号を輸送するミキサーラインのコンポーネントの種類は、MIXERLINE\_COMPONENTTYPE\_DST\_ヘッドホンです。

-   **ミキサー-線のターゲットの種類**

    ミキサーの線が転送するデータストリームの種類を示します。 たとえば、wave 出力 (レンダリング) ストリームのターゲット型は MIXERLINE\_TARGETTYPE\_WAVEOUT であり、wave 入力 (capture) ストリームのターゲット型は MIXERLINE\_TARGETTYPE\_WAVEIN です。

MIXERLINE 構造体の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

次の2つの表は、WDMAud が入力 (KSPIN\_データフロー\_) ピンをソースミキサーラインに変換する方法を示しています。 最初の表は、入力ピン**KS の pin カテゴリ GUID**が、関連付けられている MIXERLINE ターゲット型にどのようにマップされるかを示しています。

PCPIN\_記述子値 MIXERLINE 値 KS pin カテゴリ GUID ブリッジ pin?
ターゲットタイプ KSNODETYPE\_マイク

KSNODETYPE\_DESKTOP\_マイク

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_従来の\_オーディオ\_コネクタ

KSCATEGORY\_オーディオ

KSNODETYPE\_スピーカー

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_CD\_PLAYER

--

MIXERLINE\_TARGETTYPE\_未定義

KSNODETYPE\_シンセサイザー

--

MIXERLINE\_TARGETTYPE\_MIDIOUT

KSNODETYPE\_LINE\_コネクタ

--

MIXERLINE\_TARGETTYPE\_未定義

KSNODETYPE\_電話

KSNODETYPE\_電話\_ライン

KSNODETYPE\_ダウン\_回線\_電話

--

MIXERLINE\_TARGETTYPE\_未定義

KSNODETYPE\_アナログ\_コネクタ

[はい]

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_アナログ\_コネクタ

必須ではない

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_インターフェイス

[はい]

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_インターフェイス

必須ではない

MIXERLINE\_TARGETTYPE\_WAVEOUT

 

次の表は、入力ピン**KS のカテゴリ GUID**s が、関連付けられている MIXERLINE コンポーネントの種類にどのようにマップされるかを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCPIN_DESCRIPTOR の値</th>
<th align="left">MIXERLINE の値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">KS pin カテゴリ GUID</td>
<td align="left">コンポーネントの種類</td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_MICROPHONE</p>
<p>KSNODETYPE_DESKTOP_MICROPHONE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_MICROPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_LEGACY_AUDIO_CONNECTOR</p>
<p>KSCATEGORY_AUDIO</p>
<p>KSNODETYPE_SPEAKER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_WAVEOUT</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_CD_PLAYER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_COMPACTDISC</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SYNTHESIZER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_SYNTHESIZER</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_LINE_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_LINE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_TELEPHONE</p>
<p>KSNODETYPE_PHONE_LINE</p>
<p>KSNODETYPE_DOWN_LINE_PHONE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_TELEPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_ANALOG</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_ANALOG</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_DIGITAL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_DIGITAL</p></td>
</tr>
</tbody>
</table>

 

上の表では、左側の列にピンの PCPIN\_記述子の構造からピンカテゴリ GUID が指定されており、右側の列で MIXERLINE 構造体に対応する対象の型とコンポーネントの種類が指定されています。

"Bridge Pin?" というラベルが付いた列のエントリ pin がブリッジ pin であるかどうかを示します。 "Yes" は、ピン通信の種類が KSPIN\_通信\_ブリッジであることを意味します。 "No" は、ピン通信の種類が kspin\_通信\_ブリッジ以外の*Xxx*値\_\_通信であることを意味します。 Pin パラメーターをミキサーラインパラメーターに変換するときに WDMAud がピン通信の種類を無視する場合、"ブリッジピン?" エントリはダッシュ (-) です。

前の表に表示されていないすべてのピンカテゴリに対して、WDMAud は入力ピンを MIXERLINE\_\_TARGETTYPE のターゲット型を持つソースミキサー行に変換します。 MIXERLINE\_COMPONENTTYPE\_SRC\_未定義です。

次の表は、WDMAud が出力 (KSPIN\_データフロー\_出力) ピンを変換先のミキサ線に変換する方法を示しています。 列見出しは、前の表と同じ意味を持ちます。 最初の表は、出力ピン**KS のピン留めカテゴリの GUID**が、関連付けられている MIXERLINE のターゲットの種類にどのようにマップされるかを示しています。

PCPIN\_記述子値 MIXERLINE 値 KS pin カテゴリ GUID ブリッジ pin?
ターゲットタイプ KSNODETYPE\_スピーカー

KSNODETYPE\_DESKTOP\_スピーカー

KSNODETYPE\_ルーム\_スピーカー

KSNODETYPE\_通信\_スピーカー

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSCATEGORY\_オーディオ

PINNAME\_CAPTURE

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_ヘッドホン

KSNODETYPE\_ヘッド\_マウント\_\_オーディオを表示する

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_電話

KSNODETYPE\_電話\_ライン

KSNODETYPE\_ダウン\_回線\_電話

--

MIXERLINE\_TARGETTYPE\_未定義

KSNODETYPE\_アナログ\_コネクタ

[はい]

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_アナログ\_コネクタ

必須ではない

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_インターフェイス

[はい]

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_インターフェイス

必須ではない

MIXERLINE\_TARGETTYPE\_WAVEIN

 

次の表は、出力ピン**KS のピン留めカテゴリ GUID**s が、関連付けられている MIXERLINE コンポーネントの種類にどのようにマップされるかを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCPIN_DESCRIPTOR の値</th>
<th align="left">MIXERLINE の値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">KS pin カテゴリ GUID</td>
<td align="left">コンポーネントの種類</td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SPEAKER</p>
<p>KSNODETYPE_DESKTOP_SPEAKER</p>
<p>KSNODETYPE_ROOM_SPEAKER</p>
<p>KSNODETYPE_COMMUNICATION_SPEAKER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_SPEAKERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSCATEGORY_AUDIO</p>
<p>PINNAME_CAPTURE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_WAVEIN</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_HEADPHONES</p>
<p>KSNODETYPE_HEAD_MOUNTED_DISPLAY_AUDIO</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_HEADPHONES</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_TELEPHONE</p>
<p>KSNODETYPE_PHONE_LINE</p>
<p>KSNODETYPE_DOWN_LINE_PHONE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_TELEPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_SPEAKERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_WAVEIN</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_SPEAKERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_WAVEIN</p></td>
</tr>
</tbody>
</table>

 

前の表に表示されていないすべてのピンカテゴリについて、WDMAud は出力ピンを MIXERLINE\_\_TARGETTYPE のターゲットの種類と MIXERLINE\_COMPONENTTYPE のコンポーネントの種類を使用して変換先のミキサ線に変換し\_DST\_未定義です。

上の表では、ほとんどの KS ピンカテゴリ Guid に KSNODETYPE\_*Xxx*の名前が付いています。 これらの名前は、ヘッダーファイルである Ksmedia. h と Dマス Prop. h で定義されています。 (この名前付け規則の2つの出発として、\_AUDIO と PINNAME\_CAPTURE という Guid があります。これは、Ksmedia. h でも定義されています)。「[トポロジノード](topology-nodes.md)」で説明されているように、KSNODETYPE\_*Xxx* guid を使用して、KS ノードの種類を指定することもできます。 ほとんどの KSNODETYPE\_*Xxx* guid は、ピンのカテゴリまたはノードの種類のいずれかを指定しますが、両方は指定しません。 この例外は、が使用されているコンテキストに応じて、ピンカテゴリまたはノードの種類のいずれかを指定できる[**KSNODETYPE\_シンセサイザー**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)です。 ピンカテゴリを表す KSNODETYPE\_*Xxx* guid の一覧については、「[ピンカテゴリのプロパティ](pin-category-property.md)」を参照してください。 ノードの種類を表す KSNODETYPE\_*Xxx* guid の一覧については、「[オーディオトポロジノード](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-topology-nodes)」を参照してください。

KSCATEGORY\_AUDIO は、別のデュアル使用率の GUID です。 コンテキストに応じて、 **ks ピンカテゴリ guid**または**KS フィルターカテゴリ guid**として使用できます。 デバイスのインストール中、オーディオドライバーは、デバイスインターフェイスをフィルターカテゴリ KSCATEGORY\_AUDIO に登録します。 詳細については、「[オーディオアダプターのデバイスインターフェイスのインストール](installing-device-interfaces-for-an-audio-adapter.md)」を参照してください。

KSNODETYPE\_アナログ\_コネクタまたは KSNODETYPE\_SPDIF\_インターフェイスのピンカテゴリの場合、WDMAud は pin がブリッジピンであるかどうかを認識し、それに相当するミキサーラインにピンが正しく変換されるようにする必要があります。 たとえば、S/PDIF ピン (pin カテゴリ KSNODETYPE\_SPDIF\_INTERFACE) は、次の図に示す4つのミキサー線の種類のいずれかに変換されます。 この平行移動は、ピンのデータ方向 (入力または出力) とブリッジピン (yes または no) の両方に依存します。これにより、4種類のミキサー線が生成されます (in + yes、in + no、out + yes、out + no)。 図に示されている4つのミキサー線の種類は、前の表のエントリの下位ペアを表しています。

![s/pdif ピンとミキサーの線の平行移動を示す図](images/spdifpin.png)

図のオーディオデバイスの右側にある2つのストリームが S/PDIF 形式であり、左側の2つのストリームが波形式であることに注意してください。 オーディオデバイスは、2つのデジタル形式の間の変換を実行します。

SndVol32 アプリケーションは、ミキサー API のクライアントです。 ミキサ API は、トポロジ内の各ピンを変換元または変換先のミキサーラインに変換しますが、SndVol32 には表示されないことがあります。これは、ヘッダーファイル Mmsystem がミキサー API に対して定義するミキサーラインコンポーネント型のサブセットのみを認識します。 SndVol32 の詳細については、「 [SysTray と SndVol32](systray-and-sndvol32.md)」を参照してください。

 

 




