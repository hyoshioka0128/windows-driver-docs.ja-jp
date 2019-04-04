---
title: KSCATEGORY_TVAUDIO
description: KSCATEGORY_TVAUDIO
ms.assetid: a3fac238-2712-4eef-b768-4bc2ac43ec4c
keywords:
- KSCATEGORY_TVAUDIO デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_TVAUDIO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f69f125f9b47a424ce294b3096f965007e8ec9f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535730"
---
# <a name="kscategorytvaudio"></a>KSCATEGORY_TVAUDIO


KSCATEGORY_TVAUDIO[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)テレビのオーディオ デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_TVAUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{A799A802-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーは、デバイスが KSCATEGORY_TVAUDIO 機能カテゴリをサポートするオペレーティング システムに示すためにこの KSCATEGORY_TVAUDIO のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください。、 *Bdan.inf* INF ファイルでのソフトウェアのチューナー サンプルに含まれている、 *src/swtuner/algtuner* WDK のディレクトリ。

ビデオ デバイスについては、[ビデオ キャプチャ デバイス](https://msdn.microsoft.com/library/windows/hardware/ff568699)、[フィルターのグラフ例](https://msdn.microsoft.com/library/windows/hardware/ff559605)、および[エンコーダー デバイス](https://msdn.microsoft.com/library/windows/hardware/ff559535)を参照してください。

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


[**KSCATEGORY_TVTUNER**](kscategory-tvtuner.md)

 

 






