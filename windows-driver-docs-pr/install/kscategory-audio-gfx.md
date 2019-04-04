---
title: KSCATEGORY_AUDIO_GFX
description: KSCATEGORY_AUDIO_GFX
ms.assetid: 6346d7c6-9ea9-450f-af6a-44dec22bf936
keywords:
- KSCATEGORY_AUDIO_GFX デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_AUDIO_GFX
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71f42b3f9c1b423753d6e21fcd0d33057c696f33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571041"
---
# <a name="kscategoryaudiogfx"></a>KSCATEGORY_AUDIO_GFX


KSCATEGORY_AUDIO_GFX[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 機能のカテゴリをサポートする、[グローバル効果 (GFX) フィルター](https://msdn.microsoft.com/library/windows/hardware/ff536403)します。

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
<td align="left"><p>KSCATEGORY_AUDIO_GFX</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{9BAF9572-340C-11D3-ABDC-00A0C90AB16F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KS オーディオ アダプター デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_AUDIO_GFX 機能カテゴリをサポートすることを示す KSCATEGORY_AUDIO_GFX のインスタンスを登録します。

オーディオのアダプターの他のデバイスのインターフェイス クラスについては、[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff536813)を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Server 2003、Windows XP、および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





