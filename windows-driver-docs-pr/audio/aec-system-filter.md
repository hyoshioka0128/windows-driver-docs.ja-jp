---
title: AEC システム フィルター
description: AEC システム フィルター
ms.assetid: 45865e8c-7080-428f-b436-6004a8d5c011
keywords:
- アコースティック エコー キャンセル WDK オーディオ
- AEC WDK オーディオ
- NS WDK オーディオ
- ノイズの抑制 WDK オーディオ
- データ形式の WDK オーディオ、AEC システムのフィルター
- レンダリング アウト ピン WDK オーディオ
- キャプチャ アウト ピン WDK オーディオ
- レンダリングでピン WDK オーディオ
- キャプチャでピン WDK オーディオ
- WDK のオーディオ、AEC システムのフィルターをフィルター処理します。
- 接続の WDK オーディオ
- グラフの WDK オーディオ、AEC システムのフィルターをフィルター処理します。
- オーディオ フィルター グラフを WDK
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ce62b73ba99f467017bb4007ecb5335e438da2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551641"
---
# <a name="aec-system-filter"></a>AEC システム フィルター


## <span id="aec_system_filter"></span><span id="AEC_SYSTEM_FILTER"></span>


AEC システム フィルター (Aec.sys) は、ソフトウェア、アコースティック エコー キャンセル (AEC) とノイズの抑制 (NS) アルゴリズムを実装します。 このフィルターは、Windows XP 以降、標準のオペレーティング システム コンポーネントです。 DirectSoundCapture アプリケーションが有効にする方法については、AEC のシステムのフィルターの使用、Microsoft Windows SDK のマニュアルを参照してください。

### <a name="span-idconstraintsimposedbyaecsystemfilterspanspan-idconstraintsimposedbyaecsystemfilterspanspan-idconstraintsimposedbyaecsystemfilterspanconstraints-imposed-by-aec-system-filter"></a><span id="Constraints_Imposed_by_AEC_System_Filter"></span><span id="constraints_imposed_by_aec_system_filter"></span><span id="CONSTRAINTS_IMPOSED_BY_AEC_SYSTEM_FILTER"></span>AEC システム フィルターによって課される制約

AEC システム フィルターで実装されているキャプチャ効果が組み込まれているオーディオ フィルター グラフは、次の制限が適用されます。

-   AEC システムのフィルターは、PCM のデータ形式を処理するピンにのみ接続できます。

-   ビット深度は、キャプチャしたストリーム用の 16 ビットおよびレンダリング ストリーム 8 または 16 ビットである必要があります。

-   AEC システムのフィルターは、16 khz の時点ですべての内部処理を実行します。 入力と出力ストリームは、ソース率に応じて変換します。

-   (次の図を参照してください)、AEC システム フィルターのキャプチャ アウトし、レンダリングでピンで Windows XP SP1、Windows Server 2003、およびそれ以降、同じのサンプル速度をいる必要がありますが、サンプルの速度でキャプチャおよびレンダリング アウト ピン各選択できるとは無関係に、その他の pin。 16 kHz、48 kHz、44.1 kHz の場合、または 8 kHz (優先順) にサンプル速度のキャプチャにピン留めができます。 (の優先順位は、処理時間とオーディオの品質に基づくです)。16 kHz、48 kHz の場合、または 44.1 kHz、レンダリング出力ピン サンプル レートは (優先順) にできます。 レンダリング アウト pin では、8 kHz のサンプル レートはサポートされていないことに注意してください。

![aec システム フィルターのピンと接続を示す図](images/aecfilt.png)

-   AEC および NS ノード (を参照してください図[Exposing Hardware-Accelerated キャプチャ効果](exposing-hardware-accelerated-capture-effects.md)) モノラル ストリームのみを処理することができます。 キャプチャのストリームが (たとえば、2 チャンネル ステレオ) マルチ チャネルの場合は、1 つ目以外のすべてのチャネルは無視 (され破棄されます)。 レンダリング並べてモノラル ストリームのみを処理できます。

-   Windows XP SP1、Windows Server 2003、以降では、この制限は存在しません。 AEC システムが正しくキャプチャ クロックの間のハンドルの不一致をフィルター処理し、ストリームを表示し、キャプチャおよびレンダリングの別のデバイスを使用できます。

-   AEC システムのフィルターを使用する場合、 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)の混在、サンプル速度変換、3 D のサウンドおよびなどのハードウェア アクセラレータをオフにします。 ソフトウェア エミュレーションではストリームのすべての混在、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)します。 この制限は、AEC システム フィルターによって、キャプチャ ストリームからレンダリング デバイスで再生されるすべてのオーディオをキャンセルできることを確認する必要があります。

-   レンダリングにある NS ノードは線形時間インバリアントである必要があります。 またはキャプチャ側または AEC 後に、グラフの AEC または NS ノードの前に、信号処理が行われます。 これらの場所のいずれかで処理非線形または時間とともに変化のシグナルを実行することにより、AEC キャプチャ信号でエコー キャンセルことを防ぎます。

-   AEC がフィルター処理、コンピューターの AEC フィルター選択されたチャネルからエコーだけをキャンセルします。 AEC 内を通過しないチャンネルから出力されるオーディオがエコー-取り消されない。 非 AEC オーディオ チャネルのエコーが機能的には、コンピューターの横にある office でラジオを再生しているオーディオにエコーします。 AEC には、無線または非 AEC チャネルからのキャンセル (とに影響しない) のエコーがありません。

上記の要件は、すべてのカーネル ストリーミング オーディオ フィルター グラフを Aec.sys で実装されているキャプチャ効果を組み込んだに適用されます。 これらの制限には、設計と実装の AEC システム フィルターで基本的な前提条件が反映されます。 Stream の形式に対する制約は、今後の Windows のバージョンで変更可能性があります。

AEC システムのフィルターを使用する製品の設計を上記の制約を考慮する必要があります。 次の質問と回答は、これらの制約が AEC のフィルター処理の動作に影響を与えることを示します。

Q:ステレオのレンダリングには DirectSound バッファーを作成しましたが、AEC を使用しているときに同じ 2 つのチャネル サウンドします。 それはなぜか。

A:AEC は、KMixer にこの制約を満たすために mono ステレオのストリームが混在しているために、mono のストリームでのみ機能します。

Q:理由では、16 ビットの 44 kHz オーディオ サウンドなどの 16 kHz AEC を使用する場合ですか。

A:AEC のシステムのフィルターは、16 khz の時点ですべての内部処理を実行します。

Q:ハードウェア アクセラレータによる DirectSound バッファーを AEC を取得できません。

A:SysAudio ハードウェア アクセラレータを使用した、AEC が有効な場合に混在させるオフにします。

Q:AEC システムのフィルターは、古い 16 カードありますか。

A:[はい]。 8 ビットのレンダリング ストリームと、AEC システム フィルターがレンダリング アウトの組み合わせである 16 ビット キャプチャ ストリーム、同時に管理できる Blaster16 のサウンド カードが 16 ビットのレンダリングとキャプチャのストリームを同時に管理できるように、キャプチャの pin をサポートします。 新しいオーディオ カードは、レンダリングとキャプチャの両方の 16 ビット以上のビットの深さをサポートするために設計する必要があります。

### <a name="span-idsummaryofdataformatsforaecpinsspanspan-idsummaryofdataformatsforaecpinsspanspan-idsummaryofdataformatsforaecpinsspansummary-of-data-formats-for-aec-pins"></a><span id="Summary_of_Data_Formats_for_AEC_Pins"></span><span id="summary_of_data_formats_for_aec_pins"></span><span id="SUMMARY_OF_DATA_FORMATS_FOR_AEC_PINS"></span>AEC ピンの書式設定データの概要

DirectSound アプリケーションを AEC システム フィルターを使用は、サンプル速度や KMixer をサポートするサンプル サイズ、DirectSound のバッファーの選択できます。 KMixer は、AEC のシステムのフィルターに入る前に、データをアプリケーションのレンダリングのバッファーから、16 kHz mono 16 ビット形式に変換します。 同様に、KMixer は、AEC システム フィルターに出た後に 16 kHz mono 16 ビットの形式に DirectSoundCapture アプリケーションのキャプチャ バッファーに送信されるデータを変換することができます。 ただし、グラフで実行される処理の量を最小限に抑えるも最高の音質を実現する、アプリケーションする必要があります 16 kHz mono 16 ビットの形式を使用レンダリングとキャプチャの両方のバッファー。

オーディオ ハードウェア AEC システムのフィルターを使用する場合は、し、ハードウェア レンダリングの暗証番号 (pin) をサポートする必要があります。、AEC のレンダリング アウト pin でサポートされているサンプル レートの少なくとも 1 つと、AEC capt でサポートされているサンプル レートのいずれかのハードウェアのキャプチャ暗証番号 (pin) がサポートする必要があります。ure pin。 AEC の最高のパフォーマンスを実現するために、ハードウェアがサポート レートが高いだけでなく 16 kHz サンプル レートをサポートする必要があります。 16 kHz レートをサポートすることでは、ハードウェアは、AEC のシステムのフィルターは、サンプル レートの変換を行う必要性を排除することで行う必要があります処理の量を減らします。

レンダリングの AEC システム フィルターの暗証番号 (pin) は、KMixer の出力ピンに接続します。 KMixer は、レンダリングで pin を必要とする形式への入力ストリームのために必要な変換を実行します。 レンダリングの pin には、2 つのデータ形式がサポートされています。

-   16 ビットのサンプル サイズの 16 kHz mono PCM を書式設定します。

-   サンプル サイズが 8 ビットの 16 kHz mono PCM 形式

キャプチャ出力ピンには、1 つだけの形式がサポートされています。

-   16 ビットのサンプル サイズの 16 kHz mono PCM を書式設定します。

DirectSoundCapture アプリケーションのバッファーの形式が 16 ビット PCM の mono 16 kHz の場合は、AEC のキャプチャをピン留めできます KMixer をバイパス DSound.DLL (前の図を参照) に直接接続します。 それ以外の場合、AEC のキャプチャ アウト暗証番号 (pin) は、KMixer、pin を mono の 16 ビットを 16 kHz PCM ストリームをアプリケーションのキャプチャで使用するバッファー形式に変換します。 これに接続します。

AEC のレンダリング アウト暗証番号 (pin) は、次の形式のいずれかで処理できます。

-   16 kHz 16 ビット発生した PCM を 2 つのチャネル (ステレオ)

-   2 つのチャネルに 8 ビット PCM を 16 kHz

-   2 つのチャネルで 48 kHz 16 ビット PCM

-   2 つのチャネルに 8 ビット PCM を 48 kHz

-   2 つのチャネルで 44.1 kHz 16 ビット PCM

-   2 つのチャネルに 8 ビット PCM を 44.1 kHz

レンダー アウト暗証番号 (pin) は、AEC ノードからの出力ストリームの両方のチャネルに 1 つのチャネルをコピーして、ステレオ ストリームを生成します。

キャプチャにピン留めは、次の形式のいずれかで処理できます。

-   チャネルの任意の数と 16 kHz 16 ビット PCM

-   48 kHz 16 ビットの PCM で任意のチャンネル

-   44.1 kHz 16 ビットの PCM で任意のチャンネル

-   チャネルの任意の数と 8 kHz 16 ビット PCM

キャプチャにピン留めだけの最初のチャネルと使用しては無視されます (破棄)、他のユーザー。

AEC システム フィルターのピンすべては、次の表に示すようにデータ形式のパラメーター値を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KSDATARANGE メンバー</th>
<th align="left">パラメーター値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>MajorFormat</strong></p></td>
<td align="left"><p>KSDATAFORMAT_TYPE_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>サブフォーマット</strong></p></td>
<td align="left"><p>KSDATAFORMAT_SUBTYPE_PCM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>指定子</strong></p></td>
<td align="left"><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p></td>
</tr>
</tbody>
</table>

 

詳細については、 **MajorFormat**、**サブフォーマット**、および**指定子**、メンバーを参照してください[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658). 例については、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)これら 3 つのパラメーター値を使用するデータ範囲の記述子を参照してください[PCM Stream データ範囲](pcm-stream-data-range.md)します。

 

 




