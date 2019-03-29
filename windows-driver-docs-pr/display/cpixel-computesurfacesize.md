---
title: CPixel ComputeSurfaceSize メソッド
description: CPixel ComputeSurfaceSize メソッドは、サーフェスを割り当てるために必要なメモリの量を決定します。
ms.assetid: aeee0757-b381-4579-abae-1190399f3a0d
keywords:
- ディスプレイ デバイスの ComputeSurfaceSize メソッド
- ComputeSurfaceSize メソッド ディスプレイ デバイス、CPixel インターフェイス
- CPixel インターフェイス ディスプレイ デバイス、ComputeSurfaceSize メソッド
topic_type:
- apiref
api_name:
- CPixel.ComputeSurfaceSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38a0f1072efb3d4a664c053e6e1ddd61af5fce71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578273"
---
# <a name="cpixelcomputesurfacesize-method"></a>CPixel::ComputeSurfaceSize メソッド


**CPixel::ComputeSurfaceSize**メソッドは、サーフェイスの割り当てに必要なメモリの量を決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
static UINT ComputeSurfaceSize(
   UINT      cpWidth,
   UINT      cpHeight,
   D3DFORMAT Format
);
```

<a name="parameters"></a>パラメーター
----------

*cpWidth*サーフェイスのピクセル単位の幅を指定します。

*cpHeight*サーフェイスのピクセル単位の高さを指定します。

*形式*D3DFORMAT 列挙体の値を使用して、surface の形式を指定します。

<a name="return-value"></a>戻り値
------------

(バイト単位)、画面のサイズを返します。

<a name="remarks"></a>コメント
-------

D3DFORMAT の詳細については、Microsoft DirectX SDK ドキュメントを参照してください。

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

 

 





