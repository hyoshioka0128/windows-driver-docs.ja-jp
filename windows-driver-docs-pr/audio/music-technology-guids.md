---
title: 音楽テクノロジ GUID
description: 音楽テクノロジ GUID
ms.assetid: 3b7c2907-e67f-458e-809d-080dcc30be1a
keywords:
- WDM オーディオ拡張 WDK、音楽テクノロジ Guid
- 音楽テクノロジ Guid WDK オーディオ
- KSDATARANGE_MUSIC 構造体
- シンセサイザー WDK オーディオ、テクノロジの Guid
- MIDI ストリームのデータ形式の WDK オーディオ
- DirectMusic WDK のオーディオ ストリームのデータを形式します。
- Dmu は、WDK のデータ形式をストリームします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8620aca8fe141af1adb0e9a02b73b167e2ca857b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571281"
---
# <a name="music-technology-guids"></a>音楽テクノロジ GUID


## <span id="music_technology_guids"></span><span id="MUSIC_TECHNOLOGY_GUIDS"></span>


MIDI または Dmu のミニポート ドライバーでは、そのピンのそれぞれで処理できること、stream の形式の範囲を指定する必要があります。 」の説明に従って[Pin ファクトリ](pin-factories.md)、ドライバーは、型の構造体は、それぞれが 1 つまたは複数のデータ範囲の記述子の配列としてこの情報を指定します[ **KSDATARANGE\_音楽**](https://msdn.microsoft.com/library/windows/hardware/ff537097). この構造体の**テクノロジ**シンセサイザー テクノロジの種類、MIDI または DirectMusic デバイスを使用してメンバーを示します。 ミニポート ドライバーを設定できる、**テクノロジ**(左の列) の次の表に示すように GUID 値の 1 つのメンバー。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KSDATARANGE_MUSIC テクノロジ GUID</th>
<th align="left">MIDIOUTCAPS wTechnology 値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_PORT</p></td>
<td align="left"><p>MOD_MIDIPORT</p></td>
<td align="left"><p>デバイスは、片方デバイスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SYNTH</p></td>
<td align="left"><p>MOD_SYNTH</p></td>
<td align="left"><p>デバイスは、シンセサイザーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SQSYNTH</p></td>
<td align="left"><p>MOD_SQSYNTH</p></td>
<td align="left"><p>デバイスは、正方形 wave シンセサイザーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_FMSYNTH</p></td>
<td align="left"><p>MOD_FMSYNTH</p></td>
<td align="left"><p>デバイスでは、FM シンセサイザーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_MAPPER</p></td>
<td align="left"><p>MOD_MAPPER</p></td>
<td align="left"><p>デバイスは、Microsoft MIDI マッパーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSMUSIC_TECHNOLOGY_WAVETABLE</p></td>
<td align="left"><p>MOD_WAVETABLE</p></td>
<td align="left"><p>デバイスは、ハードウェアのウェーブ シンセサイザーです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSMUSIC_TECHNOLOGY_SWSYNTH</p></td>
<td align="left"><p>MOD_SWSYNTH</p></td>
<td align="left"><p>デバイスは、ソフトウェアのシンセサイザーです。</p></td>
</tr>
</tbody>
</table>

 

**MidiOutGetDevCaps**関数変換テクノロジに書き込みを行うインデックスに、ドライバーから受信した GUID、 **wTechnology**に出力する MIDIOUTCAPS 構造体のメンバー、呼び出し元。 上記の表に示す、 **wTechnology** GUID は、それぞれのテクノロジに対応する値 (中央の列)。 詳細については**midiOutGetDevCaps** MIDIOUTCAPS、Microsoft Windows SDK のマニュアルを参照するとします。

デバイスを列挙する場合、Windows マルチ メディア midiOut または midiIn API を使用して、MIDI アプリケーションは MIDI のピンが DirectMusic ピンいないを確認できます。 DirectMusic アプリケーションでは、MIDI と DirectMusic の両方の pin を確認できます。 MIDI または Dmu のミニポート ドライバーでは、MIDI 暗証番号 (pin) を識別 KSDATAFORMAT に暗証番号 (pin) のデータ範囲のサブタイプの GUID を設定して\_サブタイプ\_MIDI します。 Dmu のミニポート ドライバー KSDATAFORMAT サブタイプ GUID に設定して DirectMusic 暗証番号 (pin) を識別する\_サブタイプ\_DIRECTMUSIC します。 MIDI と DirectMusic ピンのデータ範囲の例については、[MIDI Stream データ範囲](midi-stream-data-range.md)と[DirectMusic Stream データ範囲](directmusic-stream-data-range.md)を参照してください。

説明したよう[MIDI と DirectMusic フィルター](midi-and-directmusic-filters.md)、アダプタのドライバを呼び出す、 [ **PcNewMiniport** ](https://msdn.microsoft.com/library/windows/hardware/ff537714)システム提供のミニポートのいずれかのインスタンスを作成する関数Portcls.sys でドライバー。 呼び出し元のインスタンスを作成するミニポート ドライバーを指定するには、次の表で、ドライバーの Guid のいずれかを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーの GUID</th>
<th align="left">GUID のテクノロジ</th>
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

 

上記の表の右側の列では、テクノロジ、対応するミニポート ドライバーがそのピンのデータ範囲を指定する GUID を示します。 たとえば、FmSynth ミニポート ドライバーに割り当てます GUID KSMUSIC テクノロジ\_テクノロジ\_FMSYNTH そのピンを。

片方デバイスとしてアプリケーションに、一部のウェーブ シンセサイザー デバイスが公開自体 (テクノロジ GUID KSMUSIC\_テクノロジ\_ポート)。 外部のシンセサイザーがない場合はウェーブ シンセサイザーを通じて生 MIDI バイト ストリームを再生することです。

MidiOut API がウェーブ シンセサイザー デバイスを希望するただし、(テクノロジ GUID KSMUSIC\_テクノロジ\_ウェーブ) 既定 (推奨)、MIDI 再生デバイスを選択するとします。 明示的に、片方デバイスを既定のデバイスの選択を回避します。

自体を既定のデバイスを対象にするをウェーブ デバイス生 MIDI を再生できる必要があります自体として公開ウェーブ デバイス、片方のデバイスではありません。 ただし、アダプターのドライバーは、システム提供片方ミニポート ドライバーを使用して、DMusUART、そのウェーブ シンセサイザー デバイスを管理する場合ミニポート ドライバー静的に割り当てる GUID KSMUSIC テクノロジ\_テクノロジ\_ポートへのpin。

呼び出すことによって、 [ **IMusicTechnology::SetTechnology** ](https://msdn.microsoft.com/library/windows/hardware/ff536780)メソッドでは、アダプターのドライバーは、ミニポート ドライバーのデータの範囲で、テクノロジの Guid を上書きできます。 次のコード例でアダプターのドライバーは KSMUSIC、既定値から DMusUART ミニポート ドライバーのデータの範囲でテクノロジの GUID を変更\_テクノロジ\_KSMUSIC 値に、ポート\_テクノロジ\_ウェーブ テーブル。 この新しい設定では、MPU のようなウェーブ デバイスは midiOut API には、既定の MIDI デバイスによって選択される対象。

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

アダプタのドライバを呼び出す必要があります前のコード例ではコメントで示されるように、 [ **SetTechnology** ](https://msdn.microsoft.com/library/windows/hardware/ff536780)ポート ドライバーを呼び出す前に`Init`メソッド (これは、ミニポートを呼び出しますドライバーの`Init`メソッド)。 システム提供 DMusUART と UART ミニポート ドライバー両方のサポート、 [IMusicTechnology](https://msdn.microsoft.com/library/windows/hardware/ff536778)インターフェイス。 その他のミニポート ドライバー IMusicTechnology は省略可能なサポートします。 詳細については、の実装を参照してください、 **SetTechnology** DMusUART サンプル オーディオ ドライバー Microsoft Windows Driver Kit (WDK) でのメソッド。

 

 




