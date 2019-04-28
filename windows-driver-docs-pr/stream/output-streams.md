---
title: 出力ストリーム
description: 出力ストリーム
ms.assetid: 91be637c-f195-4713-bfb0-b41c0346e390
keywords:
- 出力ストリームの WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7b2ade7a2ee476a87b46944adc8fe03f56d1fa5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372336"
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

 

カーネル モード インターフェイスでは、ビデオ ポート (VPE) の拡張機能設定の制御を提供します。 詳細については、次を参照してください。[ビデオ ポート拡張機能のバック グラウンド](https://msdn.microsoft.com/library/windows/hardware/ff570536)します。

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

 

200 (小数) でのフレーム サイズ、 **SampleSize**のメンバー、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)構造を指定する必要があります。 詳細については、次を参照してください。[クローズド キャプション ストリーム](closed-captioning-streams.md)します。

 

 




