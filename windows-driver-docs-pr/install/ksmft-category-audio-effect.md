---
title: KSMFT_CATEGORY_AUDIO_EFFECT
description: KSMFT_CATEGORY_AUDIO_EFFECT
ms.assetid: a6747c99-3c16-4833-905a-52472a854f77
keywords:
- KSMFT_CATEGORY_AUDIO_EFFECT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_AUDIO_EFFECT
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dde4bcbbb5bcd65dfdfb16d6ebe014d1bc415ec9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386036"
---
# <a name="ksmftcategoryaudioeffect"></a>KSMFT_CATEGORY_AUDIO_EFFECT


KSMFT_CATEGORY_AUDIO_EFFECT[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)(KS)、オーディオ デバイスの機能のカテゴリ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSMFT_CATEGORY_AUDIO_EFFECT</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{11064c48-3648-4ed0-932e-05ce8ac811b7}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

MFT コーデックがサポートしている AVStream ドライバーは、デバイスが KSMFT_CATEGORY_AUDIO_EFFECT 機能カテゴリをサポートするオペレーティング システムに示すためにこのデバイスのインターフェイス クラスのインスタンスを登録します。

ハードウェアのコーデック サポート AVStream デバイスのデバイスのインターフェイス クラスの詳細については、次を参照してください。 [AVStream のコーデック サポートはハードウェアの概要](https://docs.microsoft.com/windows-hardware/drivers/stream/getting-started-with-hardware-codec-support-in-avstream)します。

INF ファイルでこの機能のカテゴリを登録する方法の詳細については、次を参照してください、 *Hiddigi.inf*に含まれているファイルを、 *src\\入力\\hiddigi*サンプル。ドライバー WDK に含まれています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

 

 





