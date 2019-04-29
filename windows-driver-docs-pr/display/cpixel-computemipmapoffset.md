---
title: CPixel ComputeMipMapOffset メソッド
description: CPixel ComputeMipMapOffset メソッドは、mipmap のテクスチャのサブレベルのオフセットを決定します。
ms.assetid: f7181577-c94f-436c-8b3e-2befe89185d3
keywords:
- ディスプレイ デバイスの ComputeMipMapOffset メソッド
- ComputeMipMapOffset メソッド ディスプレイ デバイス、CPixel インターフェイス
- CPixel インターフェイス ディスプレイ デバイス、ComputeMipMapOffset メソッド
topic_type:
- apiref
api_name:
- CPixel.ComputeMipMapOffset
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 86a978b34682f7a263f07c6d782f4ef8862376f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390004"
---
# <a name="cpixelcomputemipmapoffset-method"></a>CPixel::ComputeMipMapOffset メソッド


**CPixel::ComputeMipMapOffset**メソッドは、mipmap のテクスチャのサブレベル オフセットを決定します。

<a name="syntax"></a>構文
------

```cpp
static void  ComputeMipMapOffset(
   const D3DSURFACE_DESC *pDescTopLevel,
         UINT            iLevel,
         BYTE            *pBits,
   const RECT            *pRect,
         D3DLOCKED_RECT  *pLockedRectData
);
```

<a name="parameters"></a>パラメーター
----------

*pDescTopLevel* 、D3DSURFACE へのポインター\_mipmap のテクスチャの最上位のレベルを記述する DESC 構造体。

*iLevel*オフセットが決定される mipmap のテクスチャのレベルを指定します。

*pBits* mipmap のテクスチャの最上位レベルの先頭へのポインターまたは**NULL**呼び出し元には、オフセットだけが必要な場合。

*pRect* subrectangular 領域を表す RECT 構造体へのポインターまたは**NULL**呼び出し元には、下位レベルの先頭のみが必要な場合。

*pLockedRectData* 、D3DLOCKED へのポインター\_RECT 構造体を受け取るポインターまたはロックされている四角形領域のオフセット。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

最上位レベル、および、矩形サーフェスの説明、mipmap のテクスチャのレベル、ポインターを指定**CPixel::ComputeMipMapOffset**でロックされている四角形の領域に、ポインターやオフセットを返します、 **pBits** 、D3DLOCKED のメンバー\_RECT 構造**pLockedRectData**します。

D3DLOCKED の詳細については\_RECT、D3DSURFACE\_DESC、および四角形, は、Microsoft DirectX SDK ドキュメントを参照してください。

<a name="requirements"></a>要件
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

 

 





