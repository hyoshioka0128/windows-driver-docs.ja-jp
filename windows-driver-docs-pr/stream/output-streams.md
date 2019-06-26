---
title: 出力ストリーム
description: 出力ストリーム
ms.assetid: 91be637c-f195-4713-bfb0-b41c0346e390
keywords:
- 出力ストリームの WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 732f192f3ff95a972cd9ca6941162a64a1f6585c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370396"
---
# <a name="output-streams"></a>出力ストリーム





次の表では、ビデオ ポート出力ストリーム メディアを Dvd で使用される型について説明します。

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
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVideo</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NULL</p>
<div>
 
</div>
形式ブロックがありません。</td>
</tr>
</tbody>
</table>

 

カーネル モード インターフェイスでは、ビデオ ポート (VPE) の拡張機能設定の制御を提供します。 詳細については、次を参照してください。[ビデオ ポート拡張機能のバック グラウンド](https://docs.microsoft.com/windows-hardware/drivers/display/video-port-extensions-background)します。

次の表では、クローズド キャプション (CC) 出力ストリーム メディアを Dvd で使用される型について説明します。

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
<td><p>KSDATAFORMAT_TYPE_AUXLine21Data</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_Line21_GOPPacket</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子のブロックの GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p>
<div>
 
</div>
形式ブロックがありません。</td>
</tr>
</tbody>
</table>

 

200 (小数) でのフレーム サイズ、 **SampleSize**のメンバー、 [ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)構造を指定する必要があります。 詳細については、次を参照してください。[クローズド キャプション ストリーム](closed-captioning-streams.md)します。

 

 




