---
title: KSMFT_CATEGORY_AUDIO_ENCODER
description: KSMFT_CATEGORY_AUDIO_ENCODER
ms.assetid: b8be392e-6211-46ba-8b99-edcccb7ef8fb
keywords:
- KSMFT_CATEGORY_AUDIO_ENCODER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_AUDIO_ENCODER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc017b1aae303bd55484b85c4d1b0d21cff9fa74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391693"
---
# <a name="ksmftcategoryaudioencoder"></a>KSMFT_CATEGORY_AUDIO_ENCODER


KSMFT_CATEGORY_AUDIO_ENCODER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)(KS)、オーディオ デバイスの機能のカテゴリ。

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
<td align="left"><p>KSMFT_CATEGORY_AUDIO_ENCODER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{91c64bd0-f91e-4d8c-9276-db248279d975}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

MFT コーデックがサポートしている AVStream ドライバーは、デバイスが KSMFT_CATEGORY_AUDIO_ENCODER 機能カテゴリをサポートするオペレーティング システムに示すためにこのデバイスのインターフェイス クラスのインスタンスを登録します。

ハードウェアのコーデック サポート AVStream デバイスのデバイスのインターフェイス クラスの詳細については、次を参照してください。 [AVStream のコーデック サポートはハードウェアの概要](https://msdn.microsoft.com/library/windows/hardware/gg299325)します。

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

 

 





