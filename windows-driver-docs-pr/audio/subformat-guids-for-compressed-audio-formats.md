---
title: 圧縮されたオーディオ形式のサブ形式 GUID
description: 圧縮されたオーディオ形式のサブ形式 GUID
ms.assetid: f9595d6c-952c-4266-8eb5-5c8581051d28
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d9bd4029d2cf5a21c3d3a3b6fdad4a484f8a46f
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925627"
---
# <a name="subformat-guids-for-compressed-audio-formats"></a>圧縮されたオーディオ形式のサブ形式 GUID


Windows 7 では、新しいサブフォーマット Guid が Ksmedia .h ヘッダーファイルに追加され、圧縮されたオーディオ形式がサポートされるようになりました。 サブフォーマット Guid は、データ形式の特定のサブフォーマットを示します。 これらの形式は、非圧縮オーディオのコンシューマーエレクトロニクスアソシエーション (CEA) 標準で定義されています。

CEA-861-D 標準の結果として、CEA デバイスでサポートされていないオーディオ形式は、このようなデバイスに転送されないようにする必要があります。 高解像度のマルチメディアインターフェイス (HDMI) と[DisplayPort](https://www.displayport.org/)は、CEA デバイスの例です。

ユーザーモードアクセスの場合、Guid は[WAVEFORMATEXTENSIBLE](https://docs.microsoft.com/windows/win32/api/mmreg/ns-mmreg-waveformatextensible)の**Subformat**メンバーと[WAVEFORMATEXTENSIBLE\_IEC61937](https://docs.microsoft.com/windows/win32/coreaudio/representing-formats-for-iec-61937-transmissions)の**formatext**メンバーで指定されます。 オーディオドライバーのカーネルモードアクセスの場合、Guid は、 [**Ksk datarange\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体の**datarange**メンバーに指定されます。

次の表に、使用可能な圧縮されたオーディオ形式の Guid を示します。

**注**   Windows 7 HD audio class driver では、使用可能なすべての形式がサポートされているわけではありません。 Windows 7 でサポートされている形式は、テーブルにアスタリスク (\*) が付いて示されています。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 型</th>
<th align="left">サブフォーマット GUID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"></td>
<td align="left"><p>ストリームを参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>00000000-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_WAVEFORMATEX</p></td>
<td align="left"><p>IEC 60958 PCM<em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>00000092-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL</p></td>
<td align="left"><p>AC-3</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>00000003-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_MPEG1</p></td>
<td align="left"><p>MPEG-2-1 (Layer1 & 2)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>00000004-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_MPEG3</p></td>
<td align="left"><p>MPEG 3 (レイヤー 3)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>00000005-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_MPEG2</p></td>
<td align="left"><p>MPEG 2 (Multichanel)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>00000006-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_AAC</p></td>
<td align="left"><p>高度なオーディオコード * (ADTS の MPEG-2 AAC/4)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>00000008-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DTS</p></td>
<td align="left"><p>デジタルシアターサウンド (DTS)<em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0a</p></td>
<td align="left"><p>0000000a-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL_PLUS</p></td>
<td align="left"><p>Dolby Digital Plus</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0f</p></td>
<td align="left"><p>未使用。</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

高ビットレートのオーディオサンプルパケットで送信されるオーディオ形式の Guid を次の表に示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 型</th>
<th align="left">サブフォーマット GUID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0b</p></td>
<td align="left"><p>0000000b-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DTS_HD</p></td>
<td align="left"><p>DTS-HD (24 ビット、95KHz)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0c</p></td>
<td align="left"><p>0000000c-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_MLP</p></td>
<td align="left"><p>台紙 (MLP)<em> -経線ロスレスパッキング (Dolby Digital True HD-24 ビット 196khz/最大 18m bps、8チャネル)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0e</p></td>
<td align="left"><p>00000164-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_WMA_PRO</p></td>
<td align="left"><p>Windows Media オーディオ (WMA) Pro</em></p></td>
</tr>
</tbody>
</table>

 

次の表に、サードパーティのソリューションで実装できる圧縮オーディオ形式の Guid を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 型</th>
<th align="left">サブフォーマット GUID</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>00000008-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_ATRAC</p></td>
<td align="left"><p>アダプティブ変換音響コーディング (ATRAC)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>00000009-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_ONE_BIT_AUDIO</p></td>
<td align="left"><p>1ビットオーディオ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0d</p></td>
<td align="left"><p>0000000d-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DST</p></td>
<td align="left"><p>ダイレクトストリームトランスポート (DST)</p></td>
</tr>
</tbody>
</table>

 

次のコード例は、オーディオミニポートドライバーが、完全に機能する Dolby Digital Plus デコーダーを持つ HDMI シンクで使用するために、 [**Ksk datarの\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造を定義および初期化する方法を示しています。 この型のシンクは、44.1 と 48 KHz の転送速度をサポートしています。

サンプリングレートが 48 KHz の場合、オーディオミニポートドライバーは、次のコードを使用して、 [**Ksdatarange\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造体を定義および初期化します。 このコードは、オーディオミニポートドライバーが公開するデータ範囲を示しています。

```cpp
//Define and initialize KSDATARANGE_AUDIO structure
// for use with a sample rate of 48 KHz.
KSDATARANGE_AUDIO drDDPlus48;
drDDPlus48.DataRange.FormatSize = sizeof(KSDATARANGE_AUDIO);
drDDPlus48.DataRange.Flags = 0; // Ignored.
drDDPlus48.DataRange.SampleSize = 0; // Ignored.
drDDPlus48.DataRange.Reserved = 0;
drDDPlus48.DataRange.MajorFormat = KSDATAFORMAT_TYPE_AUDIO;
drDDPlus48.DataRange.SubFormat = KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL_PLUS;
drDDPlus48.DataRange.Specifier = KSDATAFORMAT_SPECIFIER_WAVEFORMATEX;
drDDPlus48.MaximumChannels = 2
drDDPlus48.MinimumBitsPerSample = 16; // All encoded data is transmitted at
drDDPlus48.MaximumBitsPerSample = 16; // 16 bits over IEC 60958.
drDDPlus48.MinimumSampleFrequency = 192000; // 48 KHz * 4.
drDDPlus48.MaximumSampleFrequency = 192000;
```

サンプリングレートが 44.1 KHz の場合、オーディオミニポートドライバーは、次のコードを使用して、 [**Ksk datarの\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造体を定義し、初期化します。

```cpp
//Define and initialize KSDATARANGE_AUDIO structure
// for use with a sample rate of 41.1 KHz.
KSDATARANGE_AUDIO drDDPlus44;
drDDPlus44.DataRange.FormatSize = sizeof(KSDATARANGE_AUDIO);
drDDPlus44.DataRange.Flags = 0 // Ignored.
drDDPlus44.DataRange.SampleSize = 0 // Ignored.
drDDPlus44.DataRange.Reserved = 0; 
drDDPlus44.DataRange.MajorFormat = KSDATAFORMAT_TYPE_AUDIO;
drDDPlus44.DataRange.SubFormat = KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL_PLUS;
drDDPlus44.DataRange.Specifier = KSDATAFORMAT_SPECIFIER_WAVEFORMATEX;
drDDPlus44.MaximumChannels = 2
drDDPlus44.MinimumBitsPerSample = 16; // All encoded data is transmitted at
drDDPlus44.MaximumBitsPerSample = 16; // 16 bits over IEC 60958.
drDDPlus44.MinimumSampleFrequency = 176400; // 44.1 KHz * 4
drDDPlus44.MaximumSampleFrequency = 176400;
```

 

 




