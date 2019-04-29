---
title: CPixel ComputeSurfaceOffset メソッド
description: CPixel ComputeSurfaceOffset メソッドは、サーフェスの subrectangular オフセットを決定します。
ms.assetid: 3589ea80-94f8-418b-895d-c52310536e45
keywords:
- ディスプレイ デバイスの ComputeSurfaceOffset メソッド
- ComputeSurfaceOffset メソッド ディスプレイ デバイス、CPixel インターフェイス
- CPixel インターフェイス ディスプレイ デバイス、ComputeSurfaceOffset メソッド
topic_type:
- apiref
api_name:
- CPixel.ComputeSurfaceOffset
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a160240c166a36f15ef9dd7a19206d1e784f2cce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389999"
---
# <a name="cpixelcomputesurfaceoffset-method"></a>CPixel::ComputeSurfaceOffset メソッド


**CPixel::ComputeSurfaceOffset**メソッドは、サーフェイスの subrectangular オフセットを決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
static void ComputeSurfaceOffset(
   const D3DSURFACE_DESC *pDescTopLevel,
         BYTE            *pBits,
   const RECT            *pRect,
         D3DLOCKED_RECT  *pLockedRectData
);
```

<a name="parameters"></a>パラメーター
----------

*pDescTopLevel* 、D3DSURFACE へのポインター\_サーフェスを記述する DESC 構造体。

*pBits*サーフェスの先頭へのポインターまたは**NULL**呼び出し元には、オフセットだけが必要な場合。

*pRect* subrectangular 領域を表す RECT 構造体へのポインターまたは**NULL**呼び出し元には、画面の先頭のみが必要な場合。

*pLockedRectData* 、D3DLOCKED へのポインター\_RECT 構造体を受け取るポインターまたはロックされている四角形領域のオフセット。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

画面の説明、画面と、矩形の先頭へのポインターを指定**CPixel::ComputeSurfaceOffset**でロックされている四角形の領域に、ポインターやオフセットを返します、 **pBits**、D3DLOCKED のメンバー\_RECT 構造**pLockedRectData**します。

D3DLOCKED の詳細については\_RECT、D3DSURFACE\_DESC、および四角形, は、Microsoft DirectX SDK ドキュメントを参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Pixel.hpp (Pixel.hpp を含む)</td>
</tr>
</tbody>
</table>

 

 





