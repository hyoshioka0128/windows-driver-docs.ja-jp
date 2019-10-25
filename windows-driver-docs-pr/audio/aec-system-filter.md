---
title: AEC システム フィルター
description: AEC システム フィルター
ms.assetid: 45865e8c-7080-428f-b436-6004a8d5c011
keywords:
- 音響エコーキャンセル WDK オーディオ
- AEC WDK オーディオ
- NS WDK オーディオ
- ノイズ抑制 WDK オーディオ
- データ形式 WDK オーディオ、AEC システムフィルター
- レンダーピンの WDK オーディオ
- キャプチャピンの WDK オーディオ
- レンダーピン WDK オーディオ
- 取り込みピン WDK オーディオ
- WDK オーディオ、AEC システムフィルターをフィルター処理します
- WDK オーディオの接続
- グラフのフィルター WDK オーディオ、AEC システムフィルター
- オーディオフィルターグラフ WDK
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8f7655bc44c4a357fdc8cd71c052db290bc53c77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831593"
---
# <a name="aec-system-filter"></a>AEC システム フィルター


## <span id="aec_system_filter"></span><span id="AEC_SYSTEM_FILTER"></span>


AEC システムフィルター (aec) は、ソフトウェアで音響エコーキャンセル (AEC) アルゴリズムとノイズ抑制 (NS) アルゴリズムを実装します。 このフィルターは、Windows XP 以降の標準的なオペレーティングシステムコンポーネントです。 DirectSoundCapture アプリケーションが AEC システムフィルターの使用を有効にする方法の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

### <a name="span-idconstraints_imposed_by_aec_system_filterspanspan-idconstraints_imposed_by_aec_system_filterspanspan-idconstraints_imposed_by_aec_system_filterspanconstraints-imposed-by-aec-system-filter"></a><span id="Constraints_Imposed_by_AEC_System_Filter"></span><span id="constraints_imposed_by_aec_system_filter"></span><span id="CONSTRAINTS_IMPOSED_BY_AEC_SYSTEM_FILTER"></span>AEC システムフィルターによって課される制約

AEC システムフィルターに実装されているキャプチャ効果を組み込んだオーディオフィルターグラフには、次の制限が適用されます。

-   AEC システムフィルターは、PCM データ形式を処理するピンにのみ接続できます。

-   ビット深度は、キャプチャストリームの場合は16ビット、レンダーストリームの場合は8ビットまたは16ビットである必要があります。

-   AEC システムフィルターは、すべての内部処理を 16 kHz で実行します。 入力ストリームと出力ストリームは、必要に応じて変換されたソースレートです。

-   Windows XP SP1、Windows Server 2003、およびそれ以降では、AEC システムフィルターのキャプチャアウトおよびレンダリングピン (次の図を参照) のサンプルレートは同じである必要がありますが、キャプチャインピンとレンダーアウトピンのサンプルレートは、それぞれ独立して選択できます。その他のピン。 キャプチャピンのサンプル速度は、16 kHz、48 kHz、44.1 kHz、または 8 kHz のいずれかに設定できます。 (優先順位は、処理時間とオーディオ品質に基づきます)。レンダーピンのサンプル速度は、16 kHz、48 kHz、または 44.1 kHz となります (優先度順)。 レンダーピンは、サンプルレートの 8 kHz をサポートしていないことに注意してください。

![aec システムフィルターのピンと接続を示す図](images/aecfilt.png)

-   AEC および NS ノード ([ハードウェアアクセラレータのキャプチャ効果の露出](exposing-hardware-accelerated-capture-effects.md)に関する図を参照) は、monophonic ストリームのみを処理できます。 キャプチャストリームがマルチチャネル (たとえば、2チャネルステレオ) の場合、最初のチャネル以外のすべてのチャネルは無視され、破棄されます。 レンダー側で処理できるのは、monophonic ストリームだけです。

-   Windows XP SP1、Windows Server 2003、およびそれ以降では、この制限は存在しません。 AEC システムフィルターは、キャプチャストリームとレンダーストリームのクロック間の不一致を正しく処理します。また、キャプチャとレンダリングに個別のデバイスを使用できます。

-   AEC システムフィルターを使用すると、 [Sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)によって、混合、サンプルレート変換、3d spatialization などのハードウェアアクセラレータがオフになります。 ストリームの混在はすべて、 [KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)によるソフトウェアエミュレーションで行われます。 この制限は、レンダリングデバイスによって再生されるすべてのオーディオを、AEC システムフィルターによってキャプチャストリームからキャンセルできるようにするために必要です。

-   グラフのキャプチャ側の AEC または NS ノードの前、またはレンダー側の AEC または NS ノードの後に行われるすべてのシグナル処理は、線形の時間不変である必要があります。 これらの場所のいずれかで非線形または時間に変化するシグナル処理を実行すると、AEC はキャプチャシグナルのエコーをキャンセルできません。

-   AEC フィルター処理では、コンピューター内の AEC によってフィルター処理されたチャネルからのエコーのみが取り消されます。 AEC を通過しないチャネルを介して出力されるオーディオは、エコーはキャンセルされません。 AEC 以外のオーディオチャネルでのエコーは、コンピューターの横にあるオフィスのラジオで再生されるオーディオのエコーと機能的には同等です。 AEC では、ラジオまたは非 AEC チャネルからのエコーをキャンセル (および無効にする) することはできません。

上記の要件は、Aec に実装されているキャプチャ効果を組み込んだすべてのカーネルストリーミングオーディオフィルターグラフに適用されます。 これらの制限は、AEC システムフィルターの設計および実装における基本的な想定を反映しています。 ストリーム形式に対する制約は、Windows の将来のバージョンで変更される可能性があります。

AEC システムフィルターを使用する製品設計では、前述の制約を考慮する必要があります。 次の質問と回答は、これらの制約が AEC のフィルター処理の動作にどのように影響するかを示しています。

Q: ステレオレンダリング用の DirectSound バッファーを作成しましたが、AEC を使用しているときは、両方のチャンネルが同じように聞こえます。 それはなぜか。

A: AEC は mono ストリームでのみ機能するため、KMixer はこの制約を満たすためにステレオストリームを mono にミキシングします。

Q: AEC を使用すると、44-kHz、16ビットオーディオサウンド (16 kHz など) が使用されるのはなぜですか。

A: AEC システムフィルターは、16 kHz ですべての内部処理を実行します。

Q: AEC を使用してハードウェアアクセラレータの DirectSound バッファーを取得できないのはなぜですか。

A: AEC が有効になっていると、SysAudio によってハードウェアアクセラレータの混在がオフになります。

Q: AEC システムフィルターは、古い Sound Blaster 16 カードで動作しますか。

A: はい。 Sound Blaster16 カードは16ビットレンダリングストリームとキャプチャストリームを同時に管理することはできませんが、8ビットレンダリングストリームと16ビットキャプチャストリームを同時に管理できます。これは、AEC システムフィルターのレンダリングと取り込みピンのサポート。 新しいオーディオカードは、レンダリングとキャプチャの両方で16ビット以上のビット深度をサポートするように設計する必要があります。

### <a name="span-idsummary_of_data_formats_for_aec_pinsspanspan-idsummary_of_data_formats_for_aec_pinsspanspan-idsummary_of_data_formats_for_aec_pinsspansummary-of-data-formats-for-aec-pins"></a><span id="Summary_of_Data_Formats_for_AEC_Pins"></span><span id="summary_of_data_formats_for_aec_pins"></span><span id="SUMMARY_OF_DATA_FORMATS_FOR_AEC_PINS"></span>AEC の Pin のデータ形式の概要

AEC システムフィルターを有効にする DirectSound アプリケーションでは、KMixer がサポートするサンプル速度またはサンプルサイズを DirectSound バッファーに選択できます。 KMixer は、AEC システムフィルターに入る前に、アプリケーションのレンダリングバッファーから16ビット形式の mono 16 ビット形式にデータを変換します。 同様に、KMixer は、DirectSoundCapture アプリケーションのキャプチャバッファーに送信されるデータを、AEC システムフィルターが終了した後、16 kHz mono の16ビット形式に変換できます。 ただし、グラフで実行される処理の量を最小限に抑え、最高のオーディオ品質を実現するには、アプリケーションでレンダリングバッファーとキャプチャバッファーの両方に 16 kHz mono 16 ビット形式を使用する必要があります。

オーディオハードウェアが AEC システムフィルターで動作するようにするには、ハードウェアレンダリングピンが AEC レンダーピンでサポートされるサンプルレートの少なくとも1つをサポートしている必要があります。また、ハードウェアキャプチャピンは、AEC capt によってサポートされるサンプルレートの1つをサポートしている必要があります。組み込みの pin。 最適な AEC のパフォーマンスを実現するには、ハードウェアでサポートされている高料金に加えて、16 kHz サンプルレートがサポートされている必要があります。 16 kHz 率をサポートすることで、ハードウェアによって、サンプルレート変換を実行する必要がなくなるため、AEC システムフィルターが実行する必要がある処理の量が減ります。

AEC システムフィルターのレンダーピンは、KMixer の出力ピンに接続します。 KMixer は、入力ストリームを、レンダリングピンが必要とする形式に変換する必要があります。 レンダーピンは、次の2つのデータ形式のみをサポートしています。

-   16ビットのサンプルサイズを持つ 16 kHz mono PCM 形式

-   サンプルサイズが8ビットの 16 kHz mono PCM 形式

キャプチャピンは、1つの形式のみをサポートします。

-   16ビットのサンプルサイズを持つ 16 kHz mono PCM 形式

DirectSoundCapture アプリケーションのバッファー形式が 16 kHz mono 16 ビット PCM の場合、AEC キャプチャアウトピンは KMixer をバイパスし、DSound に直接接続できます (前の図を参照)。 それ以外の場合、AEC キャプチャアウトピンは KMixer に接続します。これにより、16 kHz mono 16 ビット PCM ストリームが pin から、アプリケーションのキャプチャバッファーで使用される任意の形式に変換されます。

AEC レンダーピンは、次のいずれかの形式を処理できます。

-   2つのチャネル (ステレオ) を使用した 16 kHz 16 ビット PCM

-   2つのチャネルを持つ 16 kHz 8 ビット PCM

-   48-kHz 16 ビット PCM と2つのチャネル

-   48-kHz 8 ビット PCM と2つのチャネル

-   44.1-kHz 16 ビット PCM と2つのチャネル

-   44.1-kHz 8 ビット PCM と2つのチャネル

レンダーピンは、AEC ノードから出力ストリームの両方のチャネルに1つのチャネルをコピーすることによって、ステレオストリームを生成します。

キャプチャインピンは、次のいずれかの形式を処理できます。

-   任意の数のチャネルを使用した 16 kHz 16 ビット PCM

-   48-kHz 16 ビット PCM と任意の数のチャネル

-   44.1-kHz 16 ビット PCM と任意の数のチャネル

-   任意の数のチャネルを含む 8 kHz 16 ビット PCM

キャプチャインピンは、最初のチャネルのみを使用し、他のチャネルは無視 (および破棄) します。

すべての AEC システムフィルターのピンは、次の表に示すデータ形式のパラメーター値を使用します。

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
<td align="left"><p><strong>SubFormat</strong></p></td>
<td align="left"><p>KSDATAFORMAT_SUBTYPE_PCM</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>指定子</strong></p></td>
<td align="left"><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p></td>
</tr>
</tbody>
</table>

 

**MajorFormat**、 **subformat**、および**指定子**のメンバーの詳細については、「 [**ksk datar」** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))を参照してください。 これら3つのパラメーター値を使用する[**Ksk datar\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)データ範囲記述子の例については、「 [PCM ストリームデータ範囲](pcm-stream-data-range.md)」を参照してください。

 

 




