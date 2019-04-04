---
title: KSCATEGORY_VBICODEC
description: KSCATEGORY_VBICODEC
ms.assetid: c69857e5-19ca-44aa-ae42-bc015be2b0f8
keywords:
- KSCATEGORY_VBICODEC デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_VBICODEC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: de1cf995ad3c8b3ea99057ef398afaa6beab18b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559528"
---
# <a name="kscategoryvbicodec"></a>KSCATEGORY_VBICODEC


KSCATEGORY_VBICODEC[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)帰線消去期間 (VBI) のビデオ コーデックのデバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_VBICODEC</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{07DAD660-22F1-11D1-A9F4-00C04FBBDE8F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_VBICODEC 機能カテゴリをサポートすることを示す KSCATEGORY_VBICODEC のインスタンスを登録します。

概要ビデオ デバイスについては、[ビデオ キャプチャ デバイス](https://msdn.microsoft.com/library/windows/hardware/ff568699)を参照してください。

ビデオの非表示の詳細については、[ビデオ キャプチャ デバイスからのデータのストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568268)と[VBI カテゴリ](https://msdn.microsoft.com/library/windows/hardware/ff568691)を参照してください。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

 






