---
title: DVD デコーダー関連の KS プロパティ
description: DVD デコーダー関連の KS プロパティ
ms.assetid: 97ce831e-429b-4097-a9f4-625315fe1247
keywords:
- DVD デコーダー ミニドライバー WDK、KS プロパティ
- デコーダーのミニドライバーの WDK DVD、KS プロパティ
- KS プロパティ WDK DVD デコーダー
- プロパティは、WDK DVD デコーダーを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 879a2d9a55da4cc77fbdff7e1af36fb87694ed0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387166"
---
# <a name="dvd-decoder-related-ks-properties"></a>DVD デコーダー関連の KS プロパティ





次の表では、カーネルのストリーミング プロパティ セットと DVD デコーダーに関連付けられている対応するプロパティについて説明します。

[KSPROPSETID\_AudioDecoderOut](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-audiodecoderout)プロパティは、グループ、DVD デコーダー ハードウェアからオーディオ出力に関連するプロパティをストリーミングするすべてのカーネルを設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_AudioDecoderOut KS プロパティ</th>
<th>[プロパティの説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-auddecout-modes" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDDECOUT_MODES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-auddecout-modes)"><strong>KSPROPERTY_AUDDECOUT_MODES</strong></a></p></td>
<td><p>ビットごとの PCM の 5.1 S/PDIF など、デコーダーのハードウェアでサポートされるすべての潜在的なオーディオ出力モードの組み合わせを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-auddecout-cur-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDDECOUT_CUR_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-auddecout-cur-mode)"><strong>KSPROPERTY_AUDDECOUT_CUR_MODE</strong></a></p></td>
<td><p>ステレオ アナログまたは S/PDIF など、デコーダーのハードウェアの現在のオーディオ出力モードを指定します。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_DvdSubPic](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-dvdsubpic) DVD サブピクチャ表示に関連するプロパティをストリーミングするすべてのカーネルにグループを設定するプロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_DvdSubPic KS プロパティ</th>
<th>[プロパティの説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdsubpic-palette" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_PALETTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdsubpic-palette)"><strong>KSPROPERTY_DVDSUBPIC_PALETTE</strong></a></p></td>
<td><p>サブピクチャ表示の 16 の YUV カラー パレットのエントリを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdsubpic-hli" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_HLI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdsubpic-hli)"><strong>KSPROPERTY_DVDSUBPIC_HLI</strong></a></p></td>
<td><p>色またはコントラストを持つ、変更するのには、サブピクチャの四角形を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdsubpic-composit-on" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_COMPOSIT_ON&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdsubpic-composit-on)"><strong>KSPROPERTY_DVDSUBPIC_COMPOSIT_ON</strong></a></p></td>
<td><p>有効または DVD サブピクチャの表示を無効にするかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_CopyProt](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-copyprot) dvd の収録内容のコピー防止の Macrovision に関連するプロパティをストリーミングするすべてのカーネルにグループを設定するプロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_CopyProt KS プロパティ</th>
<th>[プロパティの説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-chlg-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_CHLG_KEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-chlg-key)"><strong>KSPROPERTY_DVDCOPY_CHLG_KEY</strong></a></p></td>
<td><p>デコーダー ハードウェア レンダラーと DVD ドライブのバス チャレンジ キーを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dvd-key1" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DVD_KEY1&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dvd-key1)"><strong>KSPROPERTY_DVDCOPY_DVD_KEY1</strong></a></p></td>
<td><p>コピー防止機構の一部として、デコーダーのバスの最初のキーを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dec-key2" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DEC_KEY2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-dec-key2)"><strong>KSPROPERTY_DVDCOPY_DEC_KEY2</strong></a></p></td>
<td><p>コピー防止機構の一部として、デコーダーのバスの 2 番目のキーを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-title-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_TITLE_KEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-title-key)"><strong>KSPROPERTY_DVDCOPY_TITLE_KEY</strong></a></p></td>
<td><p>コピー防止機構の一部として、現在の dvd の収録内容のタイトルのキーを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-copy-macrovision" data-raw-source="[&lt;strong&gt;KSPROPERTY_COPY_MACROVISION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-copy-macrovision)"><strong>KSPROPERTY_COPY_MACROVISION</strong></a></p></td>
<td><p>データ ストリームの Macrovision レベルを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-region" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_REGION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-region)"><strong>KSPROPERTY_DVDCOPY_REGION</strong></a></p></td>
<td><p>コピー防止機構の一部として、言語の制限に従って現在のリージョンを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-set-copy-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-set-copy-state)"><strong>KSPROPERTY_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
<td><p>ハードウェアの DVD デコーダーのストリームのコピー状態を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-disc-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DISC_KEY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-dvdcopy-disc-key)"><strong>KSPROPERTY_DVDCOPY_DISC_KEY</strong></a></p></td>
<td><p>コピー防止機構の一部としてデコーダーのディスクのキーを指定します。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_TSRateChange](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-tsratechange)時刻スタンプ率の変更に関連するプロパティをストリーミングするすべてのカーネルにグループを設定するプロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_TSRateChange KS プロパティ</th>
<th>[プロパティの説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-simpleratechange" data-raw-source="[&lt;strong&gt;KS_AM_RATE_SimpleRateChange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-simpleratechange)"><strong>KS_AM_RATE_SimpleRateChange</strong></a></p></td>
<td><p>新しい時刻スタンプのレートを開始する開始時刻を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-exactratechange" data-raw-source="[&lt;strong&gt;KS_AM_RATE_ExactRateChange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-exactratechange)"><strong>KS_AM_RATE_ExactRateChange</strong></a></p></td>
<td><p>新しい時刻スタンプ レートを開始する「の入力」タイムスタンプを指定します。 このプロパティはまだ実装されていません。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-maxfulldatarate" data-raw-source="[&lt;strong&gt;KS_AM_RATE_MaxFullDataRate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-maxfulldatarate)"><strong>KS_AM_RATE_MaxFullDataRate</strong></a></p></td>
<td><p>最大の完全なデータ レートを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-step" data-raw-source="[&lt;strong&gt;KS_AM_RATE_Step&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-am-rate-step)"><strong>KS_AM_RATE_Step</strong></a></p></td>
<td><p>このプロパティはまだ実装されていません。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_VPConfig と KSPROPSETID\_VPVBIConfig](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig)プロパティ セットがすべてのカーネルがストリーミング ビデオ ポートの構成および垂直帰線消去期間のビデオ ポートに関連するプロパティをグループ化構成します。 両方のプロパティ セットには、同じプロパティが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_VPConfig と KSPROPSETID_VPVBIConfig KS プロパティ</th>
<th>[プロパティの説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-numconnectinfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_NUMCONNECTINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-numconnectinfo)"><strong>KSPROPERTY_VPCONFIG_NUMCONNECTINFO</strong></a></p></td>
<td><p>ビデオ ポートに電気的な接続の最大数を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-getconnectinfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_GETCONNECTINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-getconnectinfo)"><strong>KSPROPERTY_VPCONFIG_GETCONNECTINFO</strong></a></p></td>
<td><p>可能なビデオ ポート構成の配列を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-setconnectinfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SETCONNECTINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-setconnectinfo)"><strong>KSPROPERTY_VPCONFIG_SETCONNECTINFO</strong></a></p></td>
<td><p>可能な構成の配列から特定のビデオ ポート構成を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-vpdatainfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_VPDATAINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-vpdatainfo)"><strong>KSPROPERTY_VPCONFIG_VPDATAINFO</strong></a></p></td>
<td><p>ピクセルのアスペクト比率とフィールドの極性など、初期のビデオ ポートの構成を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-maxpixelrate" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_MAXPIXELRATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-maxpixelrate)"><strong>KSPROPERTY_VPCONFIG_MAXPIXELRATE</strong></a></p></td>
<td><p>特定のディメンションでのビデオ ポートの最大ピクセルのレートを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-numvideoformat" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_NUMVIDEOFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-numvideoformat)"><strong>KSPROPERTY_VPCONFIG_NUMVIDEOFORMAT</strong></a></p></td>
<td><p>ピクセル形式の最大数を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-getvideoformat" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_GETVIDEOFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-getvideoformat)"><strong>KSPROPERTY_VPCONFIG_GETVIDEOFORMAT</strong></a></p></td>
<td><p>可能なピクセル形式の配列を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-setvideoformat" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SETVIDEOFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-setvideoformat)"><strong>KSPROPERTY_VPCONFIG_SETVIDEOFORMAT</strong></a></p></td>
<td><p>可能なピクセル形式の配列から特定のピクセル形式を指定します.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-invertpolarity" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_INVERTPOLARITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-invertpolarity)"><strong>KSPROPERTY_VPCONFIG_INVERTPOLARITY</strong></a></p></td>
<td><p>ビデオ ポートの極性を反転するかどうかを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-decimationcapability" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-decimationcapability)"><strong>KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY</strong></a></p></td>
<td><p>ハードウェアが、イメージ サイズを削減できるかどうかを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-scalefactor" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SCALEFACTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-scalefactor)"><strong>KSPROPERTY_VPCONFIG_SCALEFACTOR</strong></a></p></td>
<td><p>ユーザー定義のビデオ ポートの寸法 (幅と高さを含む) を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-ddrawhandle" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DDRAWHANDLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-ddrawhandle)"><strong>KSPROPERTY_VPCONFIG_DDRAWHANDLE</strong></a></p></td>
<td><p>DirectDraw ハンドルの情報を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-videoportid" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_VIDEOPORTID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-videoportid)"><strong>KSPROPERTY_VPCONFIG_VIDEOPORTID</strong></a></p></td>
<td><p>ビデオ ポートの ID 情報を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-ddrawsurfacehandle" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DDRAWSURFACEHANDLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-ddrawsurfacehandle)"><strong>KSPROPERTY_VPCONFIG_DDRAWSURFACEHANDLE</strong></a></p></td>
<td><p>DirectDraw surface ハンドルの情報を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-surfaceparams" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SURFACEPARAMS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-vpconfig-surfaceparams)"><strong>KSPROPERTY_VPCONFIG_SURFACEPARAMS</strong></a></p></td>
<td><p>X など、画面のパラメーターを指定 y オリジンとサーフェスの声の高さ。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_Wave](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-wave)プロパティ設定グループに関連する DVD デコーダーのハードウェア、またはオーディオのループバック ケーブルを持っているアナログのテレビ チューナー アダプターの出力量を制御するプロパティをストリーミングするすべてのカーネルサウンドのアダプター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_Wave KS プロパティ</th>
<th>[プロパティの説明]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-compatible-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-compatible-capabilities)"><strong>KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES</strong></a></p></td>
<td><p>デバイスの wave 互換性のある機能、このような入力し、出力は、デバイスを受け入れるかどうかを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-input-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_INPUT_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-input-capabilities)"><strong>KSPROPERTY_WAVE_INPUT_CAPABILITIES</strong></a></p></td>
<td><p>サンプリング頻度とサンプルあたりのビット数など、デバイスのハードウェアのウェーブ入力機能を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-output-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_OUTPUT_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-output-capabilities)"><strong>KSPROPERTY_WAVE_OUTPUT_CAPABILITIES</strong></a></p></td>
<td><p>ビット/サンプルとサンプルの使用可能なメモリなど、デバイスのハードウェアのウェーブ出力機能を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-buffer" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-buffer)"><strong>KSPROPERTY_WAVE_BUFFER</strong></a></p></td>
<td><p>ループの属性、wave バッファー サイズ、wave バッファーの開始アドレスなど、デバイスのハードウェアのウェーブ バッファーの設定を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-frequency" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_FREQUENCY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-frequency)"><strong>KSPROPERTY_WAVE_FREQUENCY</strong></a></p></td>
<td><p>デバイスのハードウェアの頻度を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-volume" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_VOLUME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-volume)"><strong>KSPROPERTY_WAVE_VOLUME</strong></a></p></td>
<td><p>デバイスのハードウェアの左端と右端のボリュームの減衰を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-pan" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_PAN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-wave-pan)"><strong>KSPROPERTY_WAVE_PAN</strong></a></p></td>
<td><p>左と右にパン、デバイスのハードウェアのレベルを指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 




