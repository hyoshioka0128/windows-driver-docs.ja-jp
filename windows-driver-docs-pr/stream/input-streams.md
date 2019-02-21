---
title: 入力ストリーム
description: 入力ストリーム
ms.assetid: 0aa378d8-e7e2-4555-b541-dd1ed77b4a12
keywords:
- 入力ストリームの WDK DVD デコーダー
- パック WDK DVD の DVD デコーダー
- サブピクチャ ストリーム WDK DVD デコーダー
- SDD オーディオ入力ストリームの WDK DVD デコーダー
- DTS のオーディオ入力ストリームの WDK DVD デコーダー
- LPCM オーディオ入力ストリームの WDK DVD デコーダー
- Ac-3 WDK DVD デコーダー
- MPEG2 ビデオ入力ストリーミング WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0740694167f9aea25a7bc31b7f08d8c9ae7024a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556858"
---
# <a name="input-streams"></a>入力ストリーム





DVD の入力ストリームは、暗号化された DVD パックの配列として、ミニドライバーに提供されます。 パックは、DVD 仕様で定義されています。 Microsoft の DVD のアーキテクチャでは、「マスター クロック」パラダイムを使用して、オーディオとビデオの同期するために、パックのシステム クロックの参照 (SCR) フィールドが 0 に設定されているに注意してください。 通常、DVD デコーダーのミニドライバーのオーディオ ストリームは、マスターのクロックを提供します。 詳細については、次を参照してください。[マスター クロック](master-clock.md)します。

DVD のデータ ストリームがを通じてミニドライバーに送信される、 [ **SRB\_書き込み\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568220)要求。 SRB の要求の詳細については、次を参照してください。 [Stream 要求のブロックの処理](handling-stream-request-blocks.md)と[Stream クラス SRB 参照](https://msdn.microsoft.com/library/windows/hardware/ff568295)します。 ハードウェアがサポートするいくつかの DVD パックは、1 つの要求パケットに存在する可能性があるために、DMA をスキャッター/ギャザーします。

次の表では、DVD ムービーで使用される MPEG2 ビデオ入力ストリーム メディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主な形式の GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_MPEG2_VIDEO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_MPEG2_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の形式</p></td>
<td><p>MPEG2VIDEOINFO</p>
<div>
 
</div>
(VIDEOINFO2 構造体のスーパー セットです。 示す MPEG プロファイルとレベル)</td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される ac-3 オーディオ入力ストリーム メディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主な形式の GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_AC3_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>(変更が求められますことに注意してください)。</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の形式</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx のスーパー セット
<p>(複数の 2 つのチャネル。 記述子の Down-mix)。</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される LPCM オーディオ入力ストリーム メディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主な形式の GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_LPCM_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の形式</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される DTS オーディオ入力ストリーム メディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主な形式の GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_DTS_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>(変更が求められますことに注意してください)。</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の形式</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx のスーパー セット
<p>(複数の 2 つのチャネル。 記述子の Down-mix)。</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される SDD オーディオ入力ストリーム メディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主な形式の GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_SDDS_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>(変更が求められますことに注意してください)。</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の形式</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx のスーパー セット
<p>(複数の 2 つのチャネル。 記述子の Down-mix)。</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用されるサブピクチャ ストリーム メディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主な形式の GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_SUBPICTURE</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の形式</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

サブピクチャが強調表示、強調表示情報とパレット情報は、プロパティとして渡されます。 サブピクチャ データ ストリームは、DVD 仕様によって提供されるデータのパケットで構成されます。 パックのヘッダーが取り除かですが、引き続き提供されます。

Microsoft DVD ナビゲーター フィルター解析すべてボタンとキーボードの情報と指定のみパス 1 つの強調表示の四角形、サブピクチャ デコーダーまで特定の時点します。 その結果、強調表示情報に送信されますデコーダーが DVD のストリームに存在よりも頻繁です。 これは、DVD 仕様によって異なります。

DVD/スプリッター ナビゲーター フィルターは、キーストロークのすべての情報を処理し、新しい送信ボタンの状態変更されるたびに情報を強調表示します。 情報は、一度に 1 つのボタンの 1 つのみのモードをについて説明します。 存在する場合にその画面のピクセル座標または、サブピクチャが、表示、表示する四角形を掲載しています。 [ **KSPROPERTY\_SPHLI** ](https://msdn.microsoft.com/library/windows/hardware/ff565627)構造体には、現在選択されているボタンの現在の状態については、色およびコントラストの情報も含まれています。 形式は、DVD 仕様で定義されます。

強調表示については、データ ストリームに非同期的に到着します。 DVD デコーダーのミニドライバーが強調表示を使用する必要があります起動し、存在する場合は、サブピクチャが関連する情報を強調表示情報を関連付けるためにタイムスタンプを終了します。 DVD デコーダーのミニドライバーが要求されたタイムスタンプのサブピクチャ ストリーム情報を受信しない場合、デコーダーでは、強調表示については、スタンドアロンと、サブピクチャには適用されません前提としています。 この場合、色およびコントラストの情報に色がすべて同じと見なされますことができます。

強調表示の情報には、開始および終了タイムスタンプが含まれています。 次に 2 つの例外、その他のタイムスタンプと同じ単位で示します。0 xffffffff の開始時刻スタンプは、強調表示のプロパティは、受信時に有効と 0 xffffffff の終了時刻のスタンプは、強調表示プロパティが有効では、次の強調表示が受信されるまでは意味を意味します。

 

 




