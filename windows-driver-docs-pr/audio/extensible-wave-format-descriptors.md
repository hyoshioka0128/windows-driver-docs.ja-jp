---
title: 拡張可能な Wave 形式の記述子
description: 拡張可能な Wave 形式の記述子
ms.assetid: b80e651b-fb97-4502-8526-e844425805dc
keywords:
- wave 形式記述子の WDK オーディオ
- PCM 形式 WDK オーディオ
- WDK オーディオの wave 形式タグ
- wave ストリーム WDK オーディオ
- WDK のオーディオデータ形式
- データ形式 WDK オーディオ、wave 形式の記述子
- WDK オーディオ、wave 形式の記述子をフォーマットします
- KSDATAFORMAT 構造体
- KMixer システムドライバー WDK オーディオ、wave 形式の記述子
- WAVEFORMATEXTENSIBLE
- WAVEFORMATEX 構造体
- WDM オーディオデータ形式 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a40b01fcecca20c423dd07bd0644ba315fed6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831241"
---
# <a name="extensible-wave-format-descriptors"></a>拡張可能な Wave 形式の記述子


## <span id="extensible_wave_format_descriptors"></span><span id="EXTENSIBLE_WAVE_FORMAT_DESCRIPTORS"></span>


次の図は、wave オーディオストリームのデータ形式記述子を示しています。

![wave 形式の記述子を示す図](images/wavefmt.png)

図に示されているように、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体に続く追加の形式情報の量は、データ形式によって異なります。

オーディオシステムでは、次のようないくつかの方法でこの種類のフォーマット記述子を使用します。

-   前の図に示されているような書式記述子は、コールパラメーターとしてミニポートドライバーの**newstream**メソッドに渡されます (たとえば、「 [**IMiniportWaveCyclic:: newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)」を参照してください)。

-   [**IMiniport::D ataRangeIntersection 部分**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)メソッドの*Result の書式*指定パラメーターは、前の図に示されているような書式記述子をメソッドが書き込むバッファーを指します。

-   [**Ksk プロパティ\_ピン留め\_DATAINTERSECTION 集合**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)の get property 要求は、前の図に示されているような形式記述子を取得します。

-   [**PROPOSEDATAFORMAT 要求\_の Ksk プロパティ\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)は、前の図に示されているような形式記述子を受け入れます。

-   [**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)関数の*Connect* call パラメーターには、同様の形式が使用されます。 このパラメーターは、書式記述子も含むバッファーの先頭にある[**Kspin\_の接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)構造体を指します。 KSPIN\_CONNECT 構造体の直後にある書式記述子は、前の図に示されているような KSDATAFORMAT 構造体から始まります。

KSDATAFORMAT 構造体の後に続く書式情報は、 [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体または[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)構造体のいずれかにする必要があります。 WAVEFORMATEXTENSIBLE は、WAVEFORMATEX よりも広い範囲の形式を記述できる WAVEFORMATEX の拡張バージョンです。 WAVEFORMATEX は、WDM WAVEFORMAT 構造体の拡張バージョンです。 WAVEFORMAT は互換性のために残されていますが、どのバージョンの Microsoft Windows でも WDM オーディオサブシステムではサポートされていません。

同様に、PCMWAVEFORMAT 構造体は互換性のために残されている WAVEFORMAT の拡張バージョンですが、WDM オーディオサブシステムでは制限付きのサポートが提供されます。

WAVEFORMAT と PCMWAVEFORMAT の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

WAVEFORMAT、PCMWAVEFORMAT、WAVEFORMATEX、WAVEFORMATEXTENSIBLE という4つの wave 形式構造は、 **wFormatTag**から始まる5つのメンバーで始まります。 上の図は、これらの4つの構造体が互いに重ねて表示され、同一の構造体の部分を強調表示していることを示しています。 PCMWAVEFORMAT と WAVEFORMATEX は、 **wBitsPerSample**メンバーを追加することで WAVEFORMAT を拡張します**が、WAVEFORMATEX メンバーも**追加します。 WAVEFORMATEXTENSIBLE**では、wValidBitsPerSample を先頭**に3つのメンバーを追加して WAVEFORMATEX を拡張します。 (**サンプル**は、一部の圧縮形式では、 **wValidBitsPerSample**の代わりに、他のメンバーである**wValidSamplesPerBlock**が使用されている共用体です)。バッファー内の KSDATAFORMAT 構造体の末尾の直後にある**wFormatTag**メンバーは、KSDATAFORMAT に続く形式情報の種類を指定します。 [KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)は、次の表に示す3つのフォーマットタグのいずれかを使用する PCM 形式のみをサポートしています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">wFormatTag 値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WAVE_FORMAT_PCM</p></td>
<td align="left"><p>WAVEFORMATEX または PCMWAVEFORMAT によって指定された整数の PCM データ形式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WAVE_FORMAT_IEEE_FLOAT</p></td>
<td align="left"><p>WAVEFORMATEX によって指定された浮動小数点 PCM データ形式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WAVE_FORMAT_EXTENSIBLE</p></td>
<td align="left"><p>WAVEFORMATEXTENSIBLE によって指定された拡張データ形式。</p></td>
</tr>
</tbody>
</table>

 

実際、KMixer では、これらのタグ値で記述できる PCM 形式のサブセットのみをサポートしています (PCM 形式以外のものはサポートしていません)。 すべての PCM 形式の USB オーディオストリームが KMixer を通過するため、USB オーディオデバイス (「 [Usbaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)」を参照してください) は、このサブセットに制限されています。 (PCM 以外の USB オーディオストリームでは、KMixer をバイパスすることができます。詳細については、「 [Pcm 形式以外の Usb オーディオサポート](usb-audio-support-for-non-pcm-formats.md)」を参照してください)。ただし、Windows XP 以前では、DirectSound アプリケーションは、KMixer でサポートされていない形式をサポートする WaveCyclic および WavePci デバイスのハードウェア pin に直接接続することによって、KMixer の制限を克服できます。 詳細については、「 [WDM オーディオの DirectSound ハードウェア高速化](directsound-hardware-acceleration-in-wdm-audio.md)」を参照してください。

前の表の\_PCM タグ値の波形\_形式の意味があいまいであることに注意してください。これには、WAVEFORMATEX または PCMWAVEFORMAT 構造体のいずれかを指定できます。 ただし、これらの2つの構造体はほぼ同じです。 唯一の違いは、WAVEFORMATEX には**cbSize**メンバーが含まれており、PCMWAVEFORMAT ではないという点です。 WAVEFORMATEX 仕様によれば、 **wFormatTag** = WAVE\_FORMAT\_PCM ( **cbSize**は暗黙的にゼロ) の場合、 **cbSize**は無視されます。**cbSize**は、他のすべての形式で使用されます。 したがって、PCM 形式の場合、PCMWAVEFORMAT と WAVEFORMATEX には同じ情報が含まれ、同じように扱うことができます。

WAVEFORMATEX は、WAVEFORMATEXTENSIBLE で指定できる形式のサブセットのみを指定できます。 WAVEFORMATEX とは異なり、WAVEFORMATEXTENSIBLE は次の操作を実行できます。

1.  サンプルコンテナーのサイズとは別に、サンプルあたりのビット数を指定します。 たとえば、20ビットのサンプルは、3バイトのコンテナー内に左揃えで格納できます。 WAVEFORMATEX はサンプルのコンテナーサイズからサンプルあたりのデータビット数を区別できません。このような形式を明確に記述することはできません。

2.  マルチチャネルストリームのオーディオチャネルに特定のスピーカーの場所を割り当てます。 WAVEFORMATEX にはこの機能がないため、mono と (2 チャネル) ステレオストリームのみを適切にサポートできます。

WAVEFORMATEX によって記述されるすべての形式は、WAVEFORMATEXTENSIBLE によって記述することもできます。 WAVEFORMATEX 構造体を WAVEFORMATEXTENSIBLE に変換する方法の詳細については、「[形式タグとサブ形式の Guid 間での変換](converting-between-format-tags-and-subformat-guids.md)」を参照してください。

WAVEFORMATEX は、サンプルサイズが8または16ビットの形式を記述するのに十分ですが、WAVEFORMATEXTENSIBLE は、16ビットを超えるサンプルの有効桁数を持つ形式を適切に記述するために必要です。 2つの例を次に示します。

-   サンプルの有効桁数が24ビットのストリームでは、効率的な処理に32ビットのコンテナーサイズを使用できますが、データを損失することなくストレージの効率を向上させるために24ビットのコンテナーを使用するように変換することができます。

-   24ビットのサンプルデータでストリームを処理する場合、20ビットの精度のみを提供するレンダリングデバイスでは、ディザリングを使用して出力信号の忠実性を向上させることができます。 ただし、ディザリングによって追加の処理時間が必要になります。また、元のストリームの精度が20ビットのみの場合は、追加の処理は必要ありません。

どちらの例でも、シグナル品質を維持しながら、処理とストレージの効率性のバランスを保つことができるのは、サンプルの有効桁数とコンテナーのサイズの両方がわかっている場合のみです。

単純な形式を WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造体で明確に記述できる場合、オーディオドライバーには、形式を説明するためのいずれかの構造を選択するオプションがあります。 ただし、通常、オーディオドライバーは、8ビットまたは16ビットのサンプルで mono および (2 チャネル) ステレオ PCM 形式を指定するために WAVEFORMATEX を使用しており、一部の古いアプリケーションでは、すべてのオーディオドライバーが WAVEFORMATEX を使用してこれらの形式を指定することを想定しています。

ドライバーが WAVEFORMATEX または WAVEFORMATEXTENSIBLE 構造体のいずれかとして明確に指定できるオーディオ形式をサポートしている場合、ドライバーは、クライアントアプリケーションまたはコンポーネントが使用する2つの構造体のうち、どれを指定するかに関係なく、形式を認識する必要があります。構造体。 たとえば、オーディオデバイスが 44.1 kHz、16ビット、ステレオ PCM 形式をサポートしている場合、PROPOSEDATAFORMAT プロパティハンドラー\_のミニポートドライバーの KSK プロパティ\_ピン留めし、 **Newstream**メソッドの実装でその形式を受け入れる必要があります。形式が WAVEFORMATEX または WAVEFORMATEXTENSIBLE のいずれの構造体として指定されているかに関係なく、

フォーマットデータの処理を簡単にするために、通常、ドライバーは WAVEFORMATEXTENSIBLE 構造体を使用して、内部的に形式を表します。 この方法では、入力 WAVEFORMATEX 構造を内部 WAVEFORMATEXTENSIBLE 表現に変換したり、内部 WAVEFORMATEXTENSIBLE 表現を出力 WAVEFORMATEX 構造体に変換したりすることが必要になる場合があります。

書式記述子を WAVEFORMATEX から WAVEFORMATEXTENSIBLE に変換するときに、WAVEFORMATEX 構造体の**wFormatTag**メンバーが WAVE\_形式\_PCM または WAVE\_形式\_IEEE\_FLOAT に設定されて**いる場合は、** スピーカー\_front\_CENTER (mono ストリームの場合) またはスピーカー\_前面\_左にある、WAVEFORMATEXTENSIBLE 構造体の dwChannelMask メンバースピーカー\_フロント\_右側 (ステレオストリームの場合)。 スピーカー\_FRONT\_*XXX*定数は、ヘッダーファイル ksmedia. h で定義されています。

Windows 98 "Gold" を除くすべての Windows リリースで、KMixer は複数のチャネルを持ち、サンプルあたり最大32ビットを持つ WAVEFORMATEXTENSIBLE PCM 形式の範囲をサポートしています。

次の表に示すように、KMixer でサポートされている WAVEFORMATEX PCM 形式のサブセットは Windows リリース間で異なります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows リリース</th>
<th align="left">パックしたサンプルサイズ</th>
<th align="left">チャンネル数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98 "Gold"</p></td>
<td align="left"><p>8、16、24、および32ビット</p></td>
<td align="left"><p>マルチチャネル</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 98 SE</p></td>
<td align="left"><p>8ビットおよび16ビットのみ</p></td>
<td align="left"><p>Mono およびステレオのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98 SE + 修正プログラム</p></td>
<td align="left"><p>8、16、24、および32ビット</p></td>
<td align="left"><p>Mono およびステレオのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>8ビットおよび16ビットのみ</p></td>
<td align="left"><p>Mono およびステレオのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Me</p></td>
<td align="left"><p>8、16、24、および32ビット</p></td>
<td align="left"><p>Mono およびステレオのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>8ビットおよび16ビットのみ</p></td>
<td align="left"><p>Mono およびステレオのみ</p></td>
</tr>
</tbody>
</table>

 
WAVEFORMATEXTENSIBLE では、 **dwBitsPerSample**はコンテナーのサイズ、 **wValidBitsPerSample**はサンプルあたりの有効なデータビット数です。 コンテナーは常にメモリにバイト単位で配置され、コンテナーのサイズは8ビットの倍数として指定する必要があります。

WAVEFORMATEXTENSIBLE 構造が定義される前に、ベンダーは、公式の16ビット形式タグを形式に割り当てることができるように、各新しい wave 形式を Microsoft に登録する必要がありました。 (Format タグは、WAVEFORMATEX 構造体の**wFormatTag**メンバーに含まれています)。登録されている書式タグの一覧がパブリックヘッダーファイル Mmreg .h (たとえば、WAVE\_FORMAT\_MPEG) に表示されます。

WAVEFORMATEXTENSIBLE では、形式の登録は不要になりました。 ベンダーは、必要に応じて、新しい形式に個別に Guid を割り当てることができます。 (形式 GUID は WAVEFORMATEXTENSIBLE の**Subformat**メンバーに含まれています)。ただし、Microsoft では、パブリックヘッダーファイル Ksmedia .h (たとえば、KSDATAFORMAT\_SUBTYPE\_MPEG) で一般的な形式の Guid をいくつか紹介しています。 新しい形式の GUID を定義する前に、ベンダの KSDATAFORMAT\_SUBTYPE\_*XXX*定数の一覧をチェックして、適切な GUID が特定の形式に対して既に定義されているかどうかを確認する必要があります。

WAVEFORMATEXTENSIBLE を使用する場合は、 **wFormatTag**を WAVE\_形式に設定し、適切な形式の GUID に拡張および**サブフォーマット**\_ます。 整数 PCM 形式の場合は、 **Subformat**を KSDATAFORMAT\_SUBTYPE\_PCM に設定します。 サンプル値を浮動小数点数としてエンコードする PCM 形式の場合は、 **Subformat**を KSDATAFORMAT\_SUBTYPE\_IEEE\_FLOAT に設定します。 どちらの形式でも、 **cbSize**を**sizeof**(WAVEFORMATEXTENSIBLE) **-sizeof**(WAVEFORMATEX) に設定します。 WAVEFORMATEXTENSIBLE を使用して PCM 以外のデータ形式を記述する方法の詳細については、「 [Pcm 以外の Wave 形式のサポート](supporting-non-pcm-wave-formats.md)」を参照してください。

 

 




