---
title: 音楽テクノロジ GUID
description: 音楽テクノロジ GUID
ms.assetid: 3b7c2907-e67f-458e-809d-080dcc30be1a
keywords:
- WDM オーディオ拡張機能 WDK、ミュージックテクノロジ Guid
- 音楽テクノロジ Guid WDK オーディオ
- KSDATARANGE_MUSIC 構造体
- シンセサイザー WDK オーディオ、テクノロジ Guid
- MIDI ストリームデータ形式 WDK オーディオ
- DirectMusic WDK audio、stream データ形式
- DMus ストリームデータ形式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93fe47da2f387fb4dca311b7dce95c884f09fe9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832566"
---
# <a name="music-technology-guids"></a>音楽テクノロジ GUID


## <span id="music_technology_guids"></span><span id="MUSIC_TECHNOLOGY_GUIDS"></span>


MIDI または DMus ミニポートドライバーでは、各ピンが処理できるストリーム形式の範囲を指定する必要があります。 「 [Pin ファクトリ](pin-factories.md)」で説明されているように、ドライバーは、1つまたは複数のデータ範囲記述子の配列としてこの情報を指定します。それぞれの記述子は、型[**ksdatarange\_MUSIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)の構造です。 この構造体の**テクノロジ**メンバーは、MIDI または DirectMusic デバイスが使用するシンセサイザーテクノロジの種類を示します。 ミニポートドライバーは、次の表に示すいずれかの GUID 値に**テクノロジ**メンバーを設定できます (左側の列)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KSDATARANGE_MUSIC テクノロジ GUID</th>
<th align="left">MIDIOUTCAPS wTechnology の値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
<td align="left"><p>MOD_MIDIPORT</p></td>
<td align="left"><p>デバイスは MPU-401 デバイスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SYNTH</p></td>
<td align="left"><p>MOD_SYNTH</p></td>
<td align="left"><p>デバイスはシンセサイザーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SQSYNTH</p></td>
<td align="left"><p>MOD_SQSYNTH</p></td>
<td align="left"><p>デバイスは、正方形のシンセサイザーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
<td align="left"><p>MOD_FMSYNTH</p></td>
<td align="left"><p>デバイスは FM シンセサイザーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_MAPPER</p></td>
<td align="left"><p>MOD_MAPPER</p></td>
<td align="left"><p>デバイスは Microsoft MIDI マッパーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_WAVETABLE</p></td>
<td align="left"><p>MOD_WAVETABLE</p></td>
<td align="left"><p>デバイスはハードウェア wavetable シンセサイザーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SWSYNTH</p></td>
<td align="left"><p>MOD_SWSYNTH</p></td>
<td align="left"><p>デバイスはソフトウェアシンセサイザーです。</p></td>
</tr>
</tbody>
</table>

 

**Midioutgetdevcaps**関数は、ドライバーから受け取ったテクノロジ GUID を、呼び出し元に出力する midioutcaps 構造体の**wtechnology**メンバーに書き込むインデックスに変換します。 上の表は、各テクノロジ GUID に対応する**Wtechnology**値 (センター列) を示しています。 **Midioutgetdevcaps**と MIDIOUTCAP の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

デバイスを列挙するときに、Windows マルチメディア midiOut または Midiout API を使用する MIDI アプリケーションは、MIDI pin を参照できますが、DirectMusic pin は参照できません。 DirectMusic アプリケーションは、MIDI ピンと DirectMusic pin の両方を参照できます。 Midi または DMus ミニポートドライバーは、pin のデータ範囲のサブタイプ GUID を KSDATAFORMAT\_SUBTYPE\_MIDI に設定することにより、MIDI pin を識別します。 DMus ミニポートドライバーは、サブタイプ GUID を KSDATAFORMAT\_SUBTYPE\_DIRECTMUSIC に設定することによって、DirectMusic pin を識別します。 MIDI と DirectMusic の pin のデータ範囲の例については、「 [Midi ストリームのデータ範囲](midi-stream-data-range.md)」と「 [Directmusic ストリームのデータ範囲](directmusic-stream-data-range.md)」を参照してください。

「 [MIDI And DirectMusic Filters](midi-and-directmusic-filters.md)」で説明されているように、アダプタードライバーは[**pcnewminiport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)関数を呼び出して、Portcls にシステムが提供するミニポートドライバーの1つのインスタンスを作成します。 呼び出し元は、次の表に示すいずれかのドライバー Guid を指定して、インスタンス化するミニポートドライバーを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバー GUID</th>
<th align="left">テクノロジ GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>CLSID_MiniportDriverDMusUART</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CLSID_MiniportDriverDMusUARTCapture</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>CLSID_MiniportDriverFmSynth</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CLSID_MiniportDriverFmSynthWithVol</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>CLSID_MiniportDriverUart</strong></p></td>
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
</tr>
</tbody>
</table>

 

上の表の右側の列は、対応するミニポートドライバーがそのピンのデータ範囲で指定しているテクノロジの GUID を示しています。 たとえば、FmSynth ミニポートドライバーは、テクノロジ GUID KSMUSIC\_テクノロジ\_FMSYNTH をその pin に割り当てます。

一部の wavetable シンセサイザーデバイスは、MPU-401 デバイス (テクノロジ GUID KSMUSIC\_テクノロジ\_ポート) としてアプリケーションに公開します。 外部シンセサイザーが存在しない場合は、wavetable シンセサイザーを介して生の MIDI バイトストリームを再生できます。

ただし、midiOut API は、既定 (推奨) の MIDI 再生デバイスを選択するときに、wavetable シンセサイザーデバイス (テクノロジ GUID KSMUSIC\_テクノロジ\_WAVETABLE) を優先します。 これにより、既定のデバイスとして MPU-401 デバイスの選択が明示的に回避されます。

既定のデバイスとして使用できるようにするには、未加工の MIDI を再生できる wavetable デバイスは、wavetable デバイスとして公開する必要があります。これは、MPU-401 デバイスではありません。 ただし、アダプタードライバーがシステムによって提供されている MPU-401 ミニポートドライバーである Dマス wavetable を使用している場合、そのシンセサイザーデバイスを管理するために、そのミニポートドライバーは、テクノロジ GUID KSMUSIC\_テクノロジ\_ポートをその pin に静的に割り当てます。

[**Imusictechnology:: SetTechnology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-imusictechnology-settechnology)メソッドを呼び出すことにより、アダプタードライバーはミニポートドライバーのデータ範囲内のテクノロジ guid を上書きできます。 次のコード例では、アダプタードライバーによって Dマス Uart ドライバーのデータ範囲のテクノロジ GUID が既定値である KSMUSIC\_テクノロジ\_ポートから、WAVETABLE の値 KSMUSIC\_\_テクノロジに変更されます。 この新しい設定では、MPU のような wavetable デバイスを既定の MIDI デバイスとして midiOut API で選択できます。

```cpp
  // Create the miniport object.
  PUNKNOWN miniport;

  ntStatus = PcNewMiniport((PMINIPORT*)&miniport, CLSID_MiniportDriverDMusUART);

  // Query the miniport driver for the IMusicTechnology interface.
  IMusicTechnology* pMusicTechnology;

  if (NT_SUCCESS(ntStatus))
  {
      ntStatus = miniport->QueryInterface(IID_IMusicTechnology, (PVOID*)&pMusicTechnology);
  }

  // Set the Technology members in the DirectMusic data-range entries
  // for all the pins that are exposed by this miniport.
  // SetTechnology should be called before initializing the miniport.
  if (NT_SUCCESS(ntStatus))
  {
      ntStatus = pMusicTechnology->SetTechnology(&KSMUSIC_TECHNOLOGY_WAVETABLE);
  }
```

前のコード例のコメントに示されているように、アダプタードライバーは、ポートドライバーの `Init` メソッドを呼び出す前に、(次にミニポートドライバーの `Init` メソッドを呼び出す[**ために)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-imusictechnology-settechnology)呼び出しを呼び出す必要があります。 システム提供の Dマス Uart および UART ミニポートドライバーは、どちらも[Imusictechnology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-imusictechnology)インターフェイスをサポートしています。 その他のミニポートドライバーでは、IMusicTechnology のサポートは省略可能です。 詳細については、Microsoft Windows Driver Kit (WDK) の Dマス Uart サンプルオーディオドライバーの**settを**実装する方法に関する説明を参照してください。

 

 




