---
title: 出力ストリーム
description: 出力ストリーム
ms.assetid: 91be637c-f195-4713-bfb0-b41c0346e390
keywords:
- 出力ストリーム WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c6a6545857cceb4b747d30b19fef5ab2d55a60d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823508"
---
# <a name="output-streams"></a>出力ストリーム





次の表では、Dvd で使用されるビデオポートの出力ストリームメディアの種類について説明します。

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
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVideo</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NULL</p>
<div>
 
</div>
フォーマットブロックがありません。</td>
</tr>
</tbody>
</table>

 

カーネルモードインターフェイスは、ビデオポート拡張 (VPE) の設定を制御します。 詳細については、「 [VideoPort Extensions Background](https://docs.microsoft.com/windows-hardware/drivers/display/video-port-extensions-background)」を参照してください。

次の表では、Dvd で使用されるクローズドキャプション (CC) 出力ストリームメディアの種類について説明します。

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
<td><p>KSDATAFORMAT_TYPE_AUXLine21Data</p></td>
</tr>
<tr class="even">
<td><p>マイナー形式の GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_Line21_GOPPacket</p></td>
</tr>
<tr class="odd">
<td><p>書式指定子の GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p>
<div>
 
</div>
フォーマットブロックがありません。</td>
</tr>
</tbody>
</table>

 

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体の**SampleSize**メンバーのフレームサイズ 200 (10 進数) を指定する必要があります。 詳細については、「[クローズドキャプションストリーム](closed-captioning-streams.md)」を参照してください。

 

 




