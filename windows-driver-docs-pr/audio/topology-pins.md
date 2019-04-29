---
title: トポロジのピン
description: トポロジのピン
ms.assetid: b434e2a7-4acc-4ef1-9db9-8f1b82f68de3
keywords:
- トポロジのピンの WDK オーディオ
- ピン WDK のオーディオ、トポロジ
- S/PDIF pin 翻訳 WDK オーディオ
- WDK のオーディオのピンの変換
- KS WDK のピンのオーディオ、翻訳します。
- ピン WDK のオーディオ、記述子
- ミキサー行記述子 WDK オーディオ
- ソース ミキサー行 WDK オーディオ
- 移行先ミキサー行 WDK オーディオ
- ピンの WDK オーディオを翻訳します。
- 暗証番号 (pin) ファクトリ WDK オーディオ
- PCPIN_DESCRIPTOR 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2ec2c37f3b4244c8d17f5050eda21c0197adc78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335276"
---
# <a name="topology-pins"></a>トポロジのピン


## <span id="topology_pins"></span><span id="TOPOLOGY_PINS"></span>


[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver) KS フィルターのトポロジのピンをミキサー API がアプリケーションに公開する元とコピー先ミキサーの行に変換します。 (シンク) の入力ピンがミキサーのソース行となり (ソース) の出力ピンが宛先ミキサーの線になります。

」の説明に従って[Pin ファクトリ](pin-factories.md)、ミニポート ドライバーは、暗証番号 (pin) の記述子の型の構造体は、それぞれの配列を提供します[ **PCPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537721)です。フィルターに属する pin ファクトリをについて説明します。 各ピン留めする記述子には、次の情報が含まれています。

-   **データ フローの方向の指定子**

    データ ストリームを入力するかどうかを示します (KSPIN\_データフロー\_IN) か、終了 (KSPIN\_データフロー\_を)、暗証番号 (pin) を使用して、フィルター。

-   **KS pin カテゴリ GUID**

    Pin が所属するピン留めするカテゴリを示します。 たとえば、オーディオの再生デバイスで、ピン留めする 1 つは wave 形式デジタル オーディオ ストリームを受け付ける場合があり、スピーカーをドライブにアナログ オーディオ信号が生成するもう 1 つの pin。 ミニポート ドライバーでは、これら 2 種類のピンがピン留めする個別のカテゴリに属するものとして識別します。

-   **通信の型指定子**

    Pin をサポートする IRP の通信の種類を示します。 IRP の通信をサポートする、暗証番号 (pin) は、IRP シンクを指定できます (KSPIN\_通信\_シンク)、IRP のソース (KSPIN\_通信\_ソース)、またはその両方 (KSPIN\_通信\_両方). IRP の通信をサポートしていないピン留めできます KS フィルター グラフ内のいずれかの円周 (KSPIN\_通信\_NONE) でも、*ブリッジ pin*グラフのエンドポイントで (KSPIN\_の通信\_ブリッジ)。

ブリッジの pin の詳細については、次を参照してください。[オーディオ フィルター グラフ](audio-filter-graphs.md)します。

WDMAud は、ミニポート ドライバーの暗証番号 (pin) の記述子から情報を次の情報を含む MIXERLINE 型の構造体である、ミキサー行記述子に変換します。

-   **Mixer 行コンポーネントの種類**

    ミキサー行が変換元または変換先の行では、およびもミキサーの行の一般的な関数を示すかどうかを示します。 たとえば、コンポーネントの型を wave から生成されるアナログ信号の転送をミキサー行は出力ヘッドフォンをドライブに (表示) のストリームが MIXERLINE\_COMPONENTTYPE\_DST\_ヘッドホンします。

-   **Mixer 行対象の型**

    ミキサーの行を転送するデータ ストリームの種類を示します。 たとえば、波の対象の型は出力 (表示) ストリームは MIXERLINE\_TARGETTYPE\_WAVEOUT、およびターゲットの型を wave (キャプチャ) の入力ストリームが MIXERLINE\_TARGETTYPE\_WAVEIN します。

MIXERLINE 構造の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

WDMAud が入力を変換する方法を次の 2 つのテーブルが表示 (KSPIN\_データフロー\_IN) ピン ミキサーのソース行にします。 最初の表は、入力がピン留めする方法を示しています。 **KS pin カテゴリ GUID**s マップに関連付けられている MIXERLINE 対象の種類。

PCPIN\_記述子値 MIXERLINE 値 KS pin カテゴリ GUID ブリッジ ピン留めしますか?
対象になる種類 KSNODETYPE\_マイク

KSNODETYPE\_デスクトップ\_マイク

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_レガシ\_オーディオ\_コネクタ

KSCATEGORY\_オーディオ

KSNODETYPE\_スピーカー

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_CD\_プレーヤー

--

MIXERLINE\_TARGETTYPE\_UNDEFINED

KSNODETYPE\_シンセサイザー

--

MIXERLINE\_TARGETTYPE\_MIDIOUT

KSNODETYPE\_行\_コネクタ

--

MIXERLINE\_TARGETTYPE\_UNDEFINED

KSNODETYPE\_電話

KSNODETYPE\_PHONE\_行

KSNODETYPE\_ダウン\_行\_電話

--

MIXERLINE\_TARGETTYPE\_UNDEFINED

KSNODETYPE\_アナログ\_コネクタ

〇

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_アナログ\_コネクタ

X

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_インターフェイス

〇

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_インターフェイス

X

MIXERLINE\_TARGETTYPE\_WAVEOUT

 

次の表は、入力のピン**KS pin カテゴリ GUID**のマップに関連付けられている MIXERLINE コンポーネントの型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCPIN_DESCRIPTOR 値</th>
<th align="left">MIXERLINE 値</th>
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

 

前の表では、左の列は、暗証番号 (pin) カテゴリ ピンの PCPIN から GUID を指定します。\_記述子構造、および右の列型および MIXERLINE 構造体のコンポーネントの種類、対応するターゲットを指定します。

ブリッジのピン留めしますか?"というラベルの付いた列のエントリ pin がブリッジ暗証番号 (pin) であるかどうかを示します。 "Yes"の場合、暗証番号 (pin) の通信の種類が KSPIN であることを意味\_通信\_ブリッジです。 暗証番号 (pin) の通信の入力を"No"手段は、KSPIN\_通信\_*Xxx* KSPIN 以外の値\_通信\_ブリッジです。 WDMAud がミキサーのコマンド ライン パラメーターをブリッジ ピン留めしますか?"にピン留めするパラメーターを変換するときに、暗証番号 (pin) の通信の種類を無視する場合 エントリは、ダッシュ (-) です。

上記のテーブルに表示されないすべてのピン留めするカテゴリ WDMAud 変換 MIXERLINE のターゲット型を持つソース ミキサー行への入力ピン\_TARGETTYPE\_MIXERLINE の未定義とコンポーネントの種類\_COMPONENTTYPE\_SRC\_UNDEFINED。

次の表は、WDMAud が出力を変換する方法を示します (KSPIN\_データフロー\_アウト) 先ミキサーの行に pin。 列見出しは、上記の表のように同じ意味を持ちます。 最初の表は、出力がピン留めする方法を示しています。 **KS pin カテゴリ GUID**s マップに関連付けられている MIXERLINE 対象の種類。

PCPIN\_記述子値 MIXERLINE 値 KS pin カテゴリ GUID ブリッジ ピン留めしますか?
対象になる種類 KSNODETYPE\_スピーカー

KSNODETYPE\_デスクトップ\_スピーカー

KSNODETYPE\_ルーム\_スピーカー

KSNODETYPE\_通信\_スピーカー

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSCATEGORY\_オーディオ

PINNAME\_キャプチャ

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_ヘッドホン

KSNODETYPE\_ヘッド\_マウント済み\_表示\_オーディオ

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_電話

KSNODETYPE\_PHONE\_行

KSNODETYPE\_ダウン\_行\_電話

--

MIXERLINE\_TARGETTYPE\_UNDEFINED

KSNODETYPE\_アナログ\_コネクタ

〇

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_アナログ\_コネクタ

X

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_インターフェイス

〇

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_インターフェイス

X

MIXERLINE\_TARGETTYPE\_WAVEIN

 

次の表は、出力がピン留めする方法を示しています。 **KS pin カテゴリ GUID**s マップに関連付けられている MIXERLINE コンポーネントの型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCPIN_DESCRIPTOR 値</th>
<th align="left">MIXERLINE 値</th>
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

 

上記のテーブルに表示されないすべてのピン留めするカテゴリ WDMAud 変換 MIXERLINE のターゲット型を持つ移行先ミキサーの行を出力ピン\_TARGETTYPE\_MIXERLINE の未定義とコンポーネントの種類\_COMPONENTTYPE\_DST\_UNDEFINED。

前述の表に、KS のほとんどはカテゴリの Guid をピン留め KSNODETYPE がある\_*Xxx*名。 これらの名前は、Ksmedia.h と Dmusprop.h ヘッダー ファイルで定義されます。 (この名前付け規則からの 2 つの別れは Guid KSCATEGORY\_オーディオおよび PINNAME\_Ksmedia.h でも定義されているをキャプチャします)。」の説明に従って[トポロジ ノード](topology-nodes.md)、KSNODETYPE\_*Xxx* Guid を使用して KS ノードの種類を指定することもできます。 ほとんどの KSNODETYPE\_*Xxx* Guid 暗証番号 (pin) のカテゴリまたはノードの種類の両方ではなくいずれかを指定します。 例外は[ **KSNODETYPE\_シンセサイザー**](https://msdn.microsoft.com/library/windows/hardware/ff537203)を使用する pin カテゴリまたはされるコンテキストに応じて、ノードの種類のいずれかを指定することができます。 KSNODETYPE の一覧については\_*Xxx*暗証番号 (pin) のカテゴリを表す Guid を参照してください[Pin Category プロパティ](pin-category-property.md)します。 KSNODETYPE の一覧については\_*Xxx*ノードの型を表す Guid を参照してください[オーディオ トポロジ ノード](https://msdn.microsoft.com/library/windows/hardware/ff536219)します。

KSCATEGORY\_オーディオが別の使用状況のデュアル GUID。 いずれかとして使用できます、 **KS pin カテゴリ GUID**または**KS フィルター カテゴリ GUID**コンテキストに応じて、します。 デバイスのインストール中に、オーディオ ドライバーに登録 KSCATEGORY フィルター カテゴリで、デバイス インターフェイス\_オーディオです。 詳細については、次を参照してください。[オーディオ アダプターのデバイスのインターフェイスをインストールする](installing-device-interfaces-for-an-audio-adapter.md)します。

KSNODETYPE の暗証番号 (pin) カテゴリの\_アナログ\_コネクタまたは KSNODETYPE\_SPDIF\_インターフェイス、WDMAud を pin ではブリッジ pin ミキサー行と同等にピン留めを正しく変換するかどうかを知る必要があります。 S/PDIF pin ではたとえば、(pin カテゴリ KSNODETYPE\_SPDIF\_インターフェイス)、次の図に示す 4 つミキサー線の種類のいずれかに変換します。 ミキサーの行のどのまとめて yield 4 種類依存 (インまたはアウト) の暗証番号 (pin) のデータの方向とかどうか (はいまたは no) ブリッジ pin では、翻訳 (yes +、+ no、out + [はい]、および out + なし)。 4 つのミキサー線の種類では、上記のテーブルからエントリの下部にあるペアの図に表示されます。

![ミキサー行へのコネクター ピンの翻訳を示す図](images/spdifpin.png)

オーディオ デバイスの図の右側にある 2 つのストリームが S/PDIF 形式で、左側の 2 つのストリームが、wave 形式のことに注意してください。 オーディオ デバイスは、2 つのデジタル形式の間の変換を実行します。

SndVol32 アプリケーションは、ミキサー API のクライアントです。 API の変換、トポロジでは、ソースまたは宛先ミキサーの行が行のいずれか見つかった各ピン ミキサーは可能性があります SndVol32、ミキサー API の Mmsystem.h を定義するヘッダー ファイル ミキサー行コンポーネントの型のサブセットのみを認識するには表示されません。 SndVol32 の詳細については、次を参照してください。[システム トレイと SndVol32](systray-and-sndvol32.md)します。

 

 




