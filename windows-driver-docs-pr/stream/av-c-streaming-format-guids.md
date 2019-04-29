---
title: AV/C ストリーミング形式の GUID
description: AV/C ストリーミング形式の GUID
ms.assetid: 60f1fd59-e760-4be4-8990-e49628b76d15
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0244c82c232fd6d4f20b0b1973b7a7b3f1ffc7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323516"
---
# <a name="avc-streaming-format-guids"></a>AV/C ストリーミング形式の GUID


## <span id="ddk_av_c_streaming_format_guids_ks"></span><span id="DDK_AV_C_STREAMING_FORMAT_GUIDS_KS"></span>


ドライバーのストリーミング、カーネルのように、AV/C ストリーミングのサブユニット ドライバーには Guid の形式を使用して各ピンのサポートされるデータ形式の範囲を指定します。 ストリーミング アプリケーションは、カーネルでは、特定のデータ形式のデータ範囲の交差部分を実行するのにこれらの形式の Guid を使用します。 結果は、入力で[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)構造体。 データの積集合の詳細に説明[AVStream のデータ範囲の交差部分](https://msdn.microsoft.com/library/windows/hardware/ff558680)します。

KSDATAFORMAT 構造は、その主な形式、形式のサブタイプ、および指定子の Guid を指定します。 指定子は、メモリ内 KSDATAFORMAT 構造を次の拡張データ構造を指定します。 たとえば、データ形式が KSDATAFORMAT の主要な形式であること\_型\_インターリーブ、KSDATAFORMAT の形式のサブタイプ\_サブタイプ\_DVSD、および KSDATAFORMAT の指定子の\_指定子\_DVINFO します。 この例では拡張データ構造体は、 [ **DVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff559517)構造体。

*Avcstrm.h*ヘッダー ファイルは、次のストリーミング形式の Guid を定義します。

<span id="KSDATAFORMAT_TYPE_INTERLEAVED"></span><span id="ksdataformat_type_interleaved"></span>KSDATAFORMAT\_型\_インターリーブ  
インターリーブ オーディオとビデオ信号を指定します。 オーディオが含まれる任意のビデオ ストリームは、ストリームの種類としてこの GUID を指定する必要があります。

<span id="KSDATAFORMAT_TYPE_MPEG2_TRANSPORT_STRIDE"></span><span id="ksdataformat_type_mpeg2_transport_stride"></span>KSDATAFORMAT\_型\_MPEG2\_トランスポート\_STRIDE  
通常の 188 バイト MPEG2 パケットのサイズから逸脱する MPEG2 ストリーム型を指定します。 KSDATAFORMAT\_型\_MPEG2\_トランスポート\_STRIDE 型が IEC 61883 4 仕様に準拠しているストリームと共に使用します。 これらのストリームを使用して、 [ **MPEG2\_トランスポート\_STRIDE** ](https://msdn.microsoft.com/library/windows/hardware/ff567742)は通常の 188 バイトのパケットを異なる形式を記述するストリームのための構造をします。 DwOffset メンバーなど、MPEG2 の\_トランスポート\_ストライドは 4、188、dwPacketLength メンバーと 192 に dwStride メンバーに設定されます。

<span id="KSDATAFORMAT_SUBTYPE_DVSD"></span><span id="ksdataformat_subtype_dvsd"></span>KSDATAFORMAT\_サブタイプ\_DVSD  
4:1 を使用した 61883-2 標準定義の 25 Mbps DV 信号、IEC を指定: NTSC 信号の構造を 1 サンプリング、またはその 4 を使用して: pal 2:0 サンプリング構造体を通知します。 この形式のサブタイプでは、データ形式の拡張データの構造体として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DVSL"></span><span id="ksdataformat_subtype_dvsl"></span>KSDATAFORMAT\_サブタイプ\_DVSL  
NTSC または PAL のシグナルと同じ数の行のですが、高い圧縮率を実装する 61883 3 時間の長い play 12.5 Mbps DVSD 信号、IEC を指定します。 この形式のサブタイプでは、データ形式の拡張データの構造体として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DVHD"></span><span id="ksdataformat_subtype_dvhd"></span>KSDATAFORMAT\_サブタイプ\_DVHD  
1125 行 60 Hz NTSC シグナルまたは 1250 行 50 Hz PAL 信号など、IEC 61883 3 の高解像度 DV 信号を指定します。 この形式のサブタイプは現在サポートされていません。

<span id="KSDATAFORMAT_SUBTYPE_DV25"></span><span id="ksdataformat_subtype_dv25"></span>KSDATAFORMAT\_SUBTYPE\_DV25  
指定、SMPTE 4:1 を使用して 314 M 25 Mbps の DVCPRO ビデオ信号: NTSC と PAL の両方のシグナルを 1 サンプリング構造。 この形式のサブタイプでは、データ形式の拡張データの構造体として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DV50"></span><span id="ksdataformat_subtype_dv50"></span>KSDATAFORMAT\_サブタイプ\_DV50  
指定、SMPTE 4 を使用して 314 M 50 Mbps の DVCPRO50 ビデオ信号: NTSC と PAL の両方の信号を 2:2 サンプルの構造体。 この形式のサブタイプでは、データ形式の拡張データの構造体として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SUBTYPE_DVH1"></span><span id="ksdataformat_subtype_dvh1"></span>KSDATAFORMAT\_サブタイプ\_DVH1  
指定、SMPTE 370 M 100 Mbps 高解像度デジタル ビデオ信号、720 p (プログレッシブ) など、または 1080 i (インター レース) 信号。 この形式のサブタイプでは、データ形式の拡張データの構造体として DVINFO 構造体を使用します。

<span id="KSDATAFORMAT_SPECIFIER_DVINFO"></span><span id="ksdataformat_specifier_dvinfo"></span>KSDATAFORMAT\_指定子\_DVINFO  
次のメモリ内 KSDATAFORMAT 拡張データ構造として DVINFO 構造体を指定します。

<span id="KSDATAFORMAT_SPECIFIER_DV_AVC"></span><span id="ksdataformat_specifier_dv_avc"></span>KSDATAFORMAT\_指定子\_DV\_AVC  
次のメモリ内 KSDATAFORMAT 拡張データ構造として、DVINFO と AVCCONNECTINFO 構造を指定します。

<span id="KSDATAFORMAT_SPECIFIER_AVC"></span><span id="ksdataformat_specifier_avc"></span>KSDATAFORMAT\_指定子\_AVC  
次のメモリ内 KSDATAFORMAT 拡張データ構造として AVCCONNECTINFO 構造体を指定します。 この指定子は、形式のサブタイプによって、MPEG2TS 形式も使用できます。

<span id="KSDATAFORMAT_SPECIFIER_61883_4"></span><span id="ksdataformat_specifier_61883_4"></span>KSDATAFORMAT\_指定子\_61883\_4  
IEC に続く MPEG2 TS 形式 61883 4 のプロトコルを指定します。 この指定子は、メモリ内 KSDATAFORMAT に従うすべての拡張データ構造を使用しません。

### <a name="comments"></a>コメント

*Avcstrm.sys*と*Msdv.sys*サポート、KSDATAFORMAT\_サブタイプ\_DV25、KSDATAFORMAT\_サブタイプ\_DV50 と KSDATAFORMAT\_サブタイプ\_DVH1 形式のサブタイプでは、Windows Vista、Windows Server 2003 Service Pack 1 (SP1)、および Windows XP Service Pack 2 (SP2) のオペレーティング システム。

なお、KSDATAFORMAT\_サブタイプ\_DVSD と KSDATAFORMAT\_サブタイプ\_DV25 形式のサブタイプでは、4 を使用して互換性のある: ntsc 1:1 サンプリングします。 ただし、KSDATAFORMAT\_サブタイプ\_DV25 PAL 形式は、4 を使用: 1:1 サンプリングが、KSDATAFORMAT\_サブタイプ\_DVSD PAL 形式は、4 を使用: 2:0 サンプリング、したがって DVSD と DV25 を区別します。

サブユニット ドライバーでは、その形式のサブタイプとその拡張データ構造の組み合わせによってフレーム サイズ (サイズのサンプル) を示します。 KSDATAFORMAT の組み合わせなど\_サブタイプ\_DVSD 形式のサブタイプと DVINFO 拡張データ構造内の NTSC ビットは、120 KB の DV フレーム サイズを示します。

[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)構造に含まれる、 **FormatSize**拡張データ構造体のサイズを検証するために使用するメンバー。 つまり、有効な拡張データ構造のサイズで FormatSize equals sizeof(KSDATAFORMAT) + sizeof (拡張データ structure(s))。

次の表では、KS データ書式指定子の Guid と、対応する拡張データ構造について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KS データの書式指定子</th>
<th>拡張データで</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_DVINFO</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559517" data-raw-source="[&lt;strong&gt;DVINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559517)"><strong>DVINFO</strong></a></p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_DV_AVC</p></td>
<td><p>DVINFO と<a href="https://msdn.microsoft.com/library/windows/hardware/ff554101" data-raw-source="[&lt;strong&gt;AVCCONNECTINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554101)"> <strong>AVCCONNECTINFO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_AVC</p></td>
<td><p>AVCCONNECTINFO</p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_61883_4</p></td>
<td><p>拡張データ構造体は使用されません。</p></td>
</tr>
</tbody>
</table>

 

Microsoft Corporation が導入された、 *msdv.sys* Windows 98 se サブユニット ドライバー。 このドライバーは、カメラのモードと VTR (ビデオ テープ レコーダー) モードの両方で、MiniDV ビデオ_カメラのほとんどをサポートします。

Microsoft Corporation が導入された、 *mstape.sys* Windows me のテープのサブユニット ドライバー このドライバーは、D VHS テープ デッキと MPEG camcorder デバイスをサポートします。

**注**Microsoft から DVCPro フォーマットのデコードをサポートするコーデックは提供されません。

 

 





