---
title: AV/C ストリーミング形式の GUID
description: AV/C ストリーミング形式の GUID
ms.assetid: 60f1fd59-e760-4be4-8990-e49628b76d15
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bd11aa78568557bb2e39ae2a07054e163034d4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845579"
---
# <a name="avc-streaming-format-guids"></a>AV/C ストリーミング形式の GUID


## <span id="ddk_av_c_streaming_format_guids_ks"></span><span id="DDK_AV_C_STREAMING_FORMAT_GUIDS_KS"></span>


任意のカーネルストリーミングドライバーと同様に、AV/C ストリーミングサブユニットドライバーは、形式 Guid を使用して、各 pin に対してサポートするデータ形式の範囲を指定します。 その後、カーネルストリーミングアプリケーションは、これらの形式の Guid を使用して、特定のデータ形式のデータ範囲の共通部分を実行します。 結果は、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体に格納されます。 データの積集合は、 [AVStream のデータ範囲の交差](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)部分で詳しく説明されています。

KSDATAFORMAT 構造体は、メジャー形式、形式のサブタイプ、および指定子の Guid を指定します。 指定子は、メモリ内の KSDATAFORMAT 構造体に続く拡張データ構造体を指定します。 たとえば、データ形式のメジャー形式が KSDATAFORMAT\_TYPE\_インターリーブ、KSDATAFORMAT\_SUBTYPE の形式のサブタイプ\_DVSD、および KSDATAFORMAT\_指定子 (DVSD\_指定子) であるとします。 この場合、拡張データ構造は[**Dvinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo)構造体です。

*Avcstrm .h*ヘッダーファイルには、次のストリーミング形式の guid が定義されています。

<span id="KSDATAFORMAT_TYPE_INTERLEAVED"></span><span id="ksdataformat_type_interleaved"></span>KSDATAFORMAT\_TYPE\_インターリーブ  
インターリーブされたオーディオおよびビデオ信号を指定します。 オーディオを含むビデオストリームでは、この GUID をストリームの型として指定する必要があります。

<span id="KSDATAFORMAT_TYPE_MPEG2_TRANSPORT_STRIDE"></span><span id="ksdataformat_type_mpeg2_transport_stride"></span>KSDATAFORMAT\_TYPE\_MPEG2\_TRANSPORT\_STRIDE  
は、通常の188バイトの MPEG2 パケットサイズから逸脱した MPEG2 ストリーム型を指定します。 KSDATAFORMAT\_TYPE\_MPEG2\_TRANSPORT\_STRIDE 型は、IEC 61883-4 仕様に準拠したストリームで使用されます。 これらのストリームは、標準の188バイトパケットとは異なる形式をストリームで記述できるようにする、 [**MPEG2\_TRANSPORT\_STRIDE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_mpeg2_transport_stride)構造体を使用します。 たとえば、MPEG2\_TRANSPORT\_ストライドの dwOffset メンバーは4に設定され、dwPacketLength メンバーは188に、Dwoffset メンバーは192に設定されます。

<span id="KSDATAFORMAT_SUBTYPE_DVSD"></span><span id="ksdataformat_subtype_dvsd"></span>KSDATAFORMAT\_サブタイプ\_DVSD  
NTSC 信号に4:1:1 サンプリング構造を使用するか、PAL 信号に4:2:0 サンプリング構造を使用する、IEC 61883-2 の標準解像度 25 Mbps の DV 信号を指定します。 この形式のサブタイプは、データ形式の拡張データ構造として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DVSL"></span><span id="ksdataformat_subtype_dvsl"></span>KSDATAFORMAT\_サブタイプ\_DVSL  
IEC 61883-3 の長い再生 12.5-Mbps の DVSD 信号を指定します。これには、NTSC 信号または PAL 信号と同じ数の行がありますが、高い圧縮率が実装されています。 この形式のサブタイプは、データ形式の拡張データ構造として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DVHD"></span><span id="ksdataformat_subtype_dvhd"></span>KSDATAFORMAT\_サブタイプ\_DVHD  
IEC 61883-3 の高解像度の DV 信号 (1125 ライン 60 Hz NTSC 信号、または1250ラインの 50 Hz PAL 信号) を指定します。 この形式のサブタイプは現在サポートされていません。

<span id="KSDATAFORMAT_SUBTYPE_DV25"></span><span id="ksdataformat_subtype_dv25"></span>KSDATAFORMAT\_サブタイプ\_DV25  
NTSC 信号と PAL 信号の両方に4:1:1 サンプリング構造を使用する SMPTE 314M 25 Mbps DVCPRO ビデオ信号を指定します。 この形式のサブタイプは、データ形式の拡張データ構造として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DV50"></span><span id="ksdataformat_subtype_dv50"></span>KSDATAFORMAT\_サブタイプ\_DV50  
NTSC 信号と PAL 信号の両方に4:2:2 サンプル構造を使用する、SMPTE 314M 50-Mbps DVCPRO50 ビデオ信号を指定します。 この形式のサブタイプは、データ形式の拡張データ構造として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DVH1"></span><span id="ksdataformat_subtype_dvh1"></span>KSDATAFORMAT\_サブタイプ\_DVH1  
720p (プログレッシブ) 信号や 1080i (インターレース) シグナルなど、SMPTE 370M 100-Mbps の高解像度の DV ビデオ信号を指定します。 この形式のサブタイプは、データ形式の拡張データ構造として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SPECIFIER_DVINFO"></span><span id="ksdataformat_specifier_dvinfo"></span>KSDATAFORMAT\_指定子\_DVINFO  
DVINFO 構造体をメモリ内の KSDATAFORMAT に続く拡張データ構造体として指定します。

<span id="KSDATAFORMAT_SPECIFIER_DV_AVC"></span><span id="ksdataformat_specifier_dv_avc"></span>KSDATAFORMAT\_指定子\_DV\_AVC  
は、メモリ内の KSDATAFORMAT に続く拡張データ構造体として DVINFO および AVCCONNECTINFO 構造体を指定します。

<span id="KSDATAFORMAT_SPECIFIER_AVC"></span><span id="ksdataformat_specifier_avc"></span>KSDATAFORMAT\_指定子\_AVC  
AVCCONNECTINFO 構造体をメモリ内の KSDATAFORMAT に続く拡張データ構造体として指定します。 この指定子は、形式のサブタイプに応じて、MPEG2TS 形式で使用することもできます。

<span id="KSDATAFORMAT_SPECIFIER_61883_4"></span><span id="ksdataformat_specifier_61883_4"></span>KSDATAFORMAT\_指定子\_61883\_4  
IEC 61883-4 プロトコルに従う MPEG2 形式を指定します。 この指定子は、メモリ内の KSDATAFORMAT に従うために拡張データ構造を使用しません。

### <a name="comments"></a>コメント

*Avcstrm .sys*と*msdv .SYS*は、KSDATAFORMAT\_SUBTYPE\_DV25、KSDATAFORMAT\_SUBTYPE\_DV50 および KSDATAFORMAT\_subtype\_DVH1 Format subtype In Windows Vista、windows Server 2003 でサポートされています。Service Pack 1 (SP1)、および Windows XP Service Pack 2 (SP2) オペレーティングシステム。

KSDATAFORMAT\_SUBTYPE\_DVSD と KSDATAFORMAT\_SUBTYPE\_DV25 形式のサブタイプは、NTSC の4:1:1 サンプリングを使用して互換性があることに注意してください。 ただし、PAL 形式の KSDATAFORMAT\_SUBTYPE\_DV25 では4:1:1 サンプリングが使用されますが、KSDATAFORMAT\_のサブ\_タイプでは、PAL 形式では4:2:0 サンプリングが使用されるため、DVSD と DV25 は区別されます。

サブユニットドライバーは、その形式のサブタイプとその拡張データ構造の組み合わせによってフレームサイズ (サンプルサイズ) を示します。 たとえば、KSDATAFORMAT\_SUBTYPE\_DVSD 形式のサブタイプの組み合わせと、DVSD 拡張データ構造体の NTSC ビットセットは、120 KB の DV フレームサイズを示します。

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体には、拡張データ構造体のサイズを検証するために使用される**formatsize**メンバーが含まれています。 つまり、有効な拡張データ構造のサイズでは、FormatSize が sizeof (KSDATAFORMAT) + sizeof (拡張データ構造体) と等しくなります。

次の表では、KS データ形式指定子の Guid と、それらに対応する拡張データ構造について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KS データ書式指定子</th>
<th>拡張データ構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_DVINFO</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo" data-raw-source="[&lt;strong&gt;DVINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo)"><strong>DVINFO</strong></a></p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_DV_AVC</p></td>
<td><p>DVINFO と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo" data-raw-source="[&lt;strong&gt;AVCCONNECTINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)"> <strong>Avcconnectinfo</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_AVC</p></td>
<td><p>AVCCONNECTINFO</p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_61883_4</p></td>
<td><p>拡張データ構造が使用されていません</p></td>
</tr>
</tbody>
</table>

 

Microsoft Corporation は、Windows 98 SE で*msdv .sys サブシステム*ドライバーを導入しました。 このドライバーは、カメラモードと VTR (ビデオテープレコーダー) モードの両方で、ほとんどの MiniDV ビデオカメラをサポートしています。

Microsoft Corporation は、Windows Me で*mstape*テープサブシステムドライバーを導入しました。 このドライバーは、D-VHS tape デッキと MPEG カムコーダーデバイスをサポートしています。

**メモ**Microsoft は、DVCPro 形式デコードをサポートするコーデックを提供していません。

 

 





