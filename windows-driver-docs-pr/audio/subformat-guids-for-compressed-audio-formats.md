---
title: 圧縮されたオーディオ形式のサブ形式 GUID
description: 圧縮されたオーディオ形式のサブ形式 GUID
ms.assetid: f9595d6c-952c-4266-8eb5-5c8581051d28
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78aaf7021bd163df49c1da399a43b40d059d2db8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354245"
---
# <a name="subformat-guids-for-compressed-audio-formats"></a>圧縮されたオーディオ形式のサブ形式 GUID


Windows 7 では、圧縮されたオーディオ形式のサポートを提供する Ksmedia.h ヘッダー ファイルに新しいサブフォーマット Guid が追加されました。 サブフォーマット Guid では、データ形式の特定のサブフォーマットを示します。 これらの形式は、非圧縮オーディオの Consumer Electronics アソシエーション (CEA) 標準で定義されます。

CEA-d 861 standard では、結果として、CEA デバイスでサポートされていないオーディオの形式がこのようなデバイスに転送されないことを確認する必要があります。 高品位のマルチ メディア インターフェイス (HDMI) と[ディスプレイ ポート等](https://www.displayport.org/)CEA デバイスの例を示します。

ユーザー モードへのアクセスの Guid がで指定された、**サブフォーマット**のメンバー [WAVEFORMATEXTENSIBLE](https://go.microsoft.com/fwlink/p/?linkid=142020)し、 **FormatExt**のメンバー [WAVEFORMATEXTENSIBLE\_IEC61937](https://go.microsoft.com/fwlink/p/?linkid=142021)します。 オーディオ ドライバーのカーネル モードによるアクセスは、Guid がで指定された、 **DataRange**のメンバー、 [ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体

使用可能な圧縮オーディオ形式の Guid は、次の表に一覧表示されます。

**注**   Windows 7 の HD オーディオ クラス ドライバーによって使用可能なすべての形式がサポートされています。 Windows 7 でサポートされる形式は、テーブルには、アスタリスクで示されています (\*)。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 型</th>
<th align="left">GUID を subFormat します。</th>
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
<td align="left"><p>Mpeg-1 (レイヤー 1 (& a) 2)。</p></td>
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
<td align="left"><p>Mpeg-2 (Multichanel)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>00000006-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_AAC</p></td>
<td align="left"><p>高度なオーディオ コーディング * (mpeg-4 2 の AAC ADTS で)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>00000008-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DTS</p></td>
<td align="left"><p>デジタル シアター サウンド (DTS)<em></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0a</p></td>
<td align="left"><p>0000000a-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_DIGITAL_PLUS</p></td>
<td align="left"><p>ドルビー デジタル プラス</em></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0f</p></td>
<td align="left"><p>未使用。</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

パケットは、次の表に記載高のビット レート オーディオのサンプルで送信されるオーディオ形式の Guid。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 型</th>
<th align="left">GUID を subFormat します。</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0b</p></td>
<td align="left"><p>0000000b-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DTS_HD</p></td>
<td align="left"><p>DTS HD (24 ビット、95 KHz)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0c</p></td>
<td align="left"><p>0000000c-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DOLBY_MLP</p></td>
<td align="left"><p>MAT(MLP)<em> -経線ロスレス パッキング (ドルビー デジタル True HD - 24 ビット 196 KHz/最大 18 M bps、チャネル 8)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0e</p></td>
<td align="left"><p>00000164-0000-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_WMA_PRO</p></td>
<td align="left"><p>Windows Media オーディオ (WMA) Pro</em></p></td>
</tr>
</tbody>
</table>

 

サード パーティ製のソリューションで実装できる圧縮のオーディオ形式の Guid は、次の表に一覧表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CEA 861 型</th>
<th align="left">GUID を subFormat します。</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>00000008-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_ATRAC</p></td>
<td align="left"><p>適応型の変換の音響 (ATRAC) のコーディング</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>00000009-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_ONE_BIT_AUDIO</p></td>
<td align="left"><p>1 ビット オーディオ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0d</p></td>
<td align="left"><p>0000000d-0cea-0010-8000-00aa00389b71</p>
<p>KSDATAFORMAT_SUBTYPE_IEC61937_DST</p></td>
<td align="left"><p>直接 Stream トランスポート (DST)</p></td>
</tr>
</tbody>
</table>

 

次のコード例は、オーディオのミニポート ドライバーの定義し、初期化を示しています、 [ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)を持つ完全に機能 Dolby Digital HDMI シンクで使用するための構造。さらにデコーダー。 このタイプのシンクには、44.1 と 48 KHz の転送速度がサポートされています。

オーディオのミニポート ドライバー 48 KHz のサンプリング レートの定義を初期化し、次のコードを使用して、 [ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体。 このコードは、オーディオのミニポート ドライバーを公開するデータ範囲を示しています。

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

オーディオのミニポート ドライバーのサンプリング レート 44.1 KHz については、定義を初期化し、次のコードを使用して、 [ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体。

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

 

 




