---
title: 入力ストリーム
description: 入力ストリーム
ms.assetid: 0aa378d8-e7e2-4555-b541-dd1ed77b4a12
keywords:
- 入力ストリーム WDK DVD デコーダー
- DVD パック WDK DVD デコーダー
- サブピクチャストリーム WDK DVD デコーダー
- SDDS オーディオ入力ストリーム WDK DVD デコーダー
- DTS オーディオ入力ストリーム WDK DVD デコーダー
- LPCM オーディオ入力ストリーム WDK DVD デコーダー
- AC 3 WDK DVD デコーダー
- MPEG2 ビデオ入力ストリーム WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 427db085c4e0884aca43c14def259b757ad07e94
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845567"
---
# <a name="input-streams"></a>入力ストリーム





DVD 入力ストリームは、暗号化された DVD パックの配列としてミニドライバーに提供されます。 パックは、DVD 仕様で定義されています。 Microsoft の DVD アーキテクチャではオーディオとビデオの同期に "マスタークロック" パラダイムが使用されるため、パックのシステムクロックリファレンス (SCR) フィールドは0に設定されていることに注意してください。 通常、DVD デコーダーミニドライバーのオーディオストリームでは、マスタークロックが提供されます。 詳細については、「[マスタークロック](master-clock.md)」を参照してください。

DVD データストリームは、 [**SRB\_WRITE\_data**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-write-data)要求を介してミニドライバーに送信されます。 SRB 要求の詳細については、「[ストリーム要求ブロック](handling-stream-request-blocks.md)と[ストリームクラス SRB 参照](https://docs.microsoft.com/windows-hardware/drivers/stream/stream-class-srb-reference)の処理」を参照してください。 1つの要求パケットにいくつかの DVD パックが存在する可能性があるため、ハードウェアはスキャッター/ギャザー DMA をサポートする必要があります。

次の表では、DVD ムービーで使用される MPEG2 ビデオ入力ストリームメディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メジャー形式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_MPEG2_VIDEO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_MPEG2_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の書式設定</p></td>
<td><p>MPEG2VIDEOINFO</p>
<div>
 
</div>
(VIDEOINFO2 構造体のスーパーセット。 MPEG プロファイルとレベルも示します。)</td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される AC 3 オーディオ入力ストリームメディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メジャー形式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_AC3_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>(これは変更される可能性があることに注意してください)。</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の書式設定</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx のスーパーセット
<p>(2 つ以上のチャネル。 ダウンミックス記述子。)</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される LPCM オーディオ入力ストリームメディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メジャー形式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_LPCM_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の書式設定</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される DTS オーディオ入力ストリームメディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メジャー形式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_DTS_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>(これは変更される可能性があることに注意してください)。</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の書式設定</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx のスーパーセット
<p>(2 つ以上のチャネル。 ダウンミックス記述子。)</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用される SDDS オーディオ入力ストリームメディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メジャー形式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_SDDS_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>(これは変更される可能性があることに注意してください)。</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の書式設定</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx のスーパーセット
<p>(2 つ以上のチャネル。 ダウンミックス記述子。)</p></td>
</tr>
</tbody>
</table>

 

次の表では、DVD ムービーで使用されるサブピクチャストリームメディアの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>メジャー形式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_SUBPICTURE</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p>ブロック構造の書式設定</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

サブピクチャの強調表示では、パレット情報と強調表示の情報がプロパティとして渡されます。 サブピクチャデータストリームは、DVD 仕様によって提供されるデータのパケットで構成されます。 パックヘッダーは削除されますが、まだ提供されています。

Microsoft が提供する DVD ナビゲーターフィルターでは、すべてのボタンとキーボード情報が解析され、任意の時点でサブピクチャデコーダーに1つのハイライト四角形のみが渡されます。 その結果、強調表示情報は、DVD ストリームに存在するよりも頻繁にデコーダーに送信されます。 これは DVD 仕様とは異なります。

DVD ナビゲーター/スプリッターフィルターでは、すべてのキーストローク情報が処理され、ボタンの状態が変化するたびに新しい強調表示情報が送信されます。 この情報には、一度に1つのボタンの1つのモードのみが記述されています。 画面のピクセル座標で表示される四角形、またはサブピクチャの表示 (存在する場合) が含まれます。 [**Ksk プロパティ\_SPHLI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)構造体には、現在選択されているボタンの現在の状態に対してのみ、色とコントラストの情報が含まれています。 形式は DVD 仕様で定義されています。

強調表示情報は、データストリームに非同期に到着します。 DVD デコーダーミニドライバーは、強調表示の開始時刻と終了時刻のタイムスタンプを使用して、強調表示情報を関連するサブピクチャ情報 (存在する場合) に関連付ける必要があります。 DVD デコーダーミニドライバーが要求されたタイムスタンプのサブピクチャストリーム情報を受信していない場合、デコーダーは、強調表示情報がスタンドアロンであり、サブピクチャには適用されないと見なします。 この場合、色とコントラストの情報はすべて同じ色であると見なすことができます。

強調表示の情報には、開始時刻と終了タイムスタンプが含まれます。 これらは、他のタイムスタンプと同じ単位になります。ただし、2つの例外があります。 "0xFFFFFFFF の開始タイムスタンプ" は、強調表示時に [強調表示] プロパティが有効であることを意味します。また、0xFFFFFFFF の終了タイムスタンプは、強調表示のプロパティが次の強調表示になるまで有効です。受け取ら.

 

 




