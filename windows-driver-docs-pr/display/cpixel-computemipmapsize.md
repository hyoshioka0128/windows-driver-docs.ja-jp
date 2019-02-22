---
title: CPixel ComputeMipMapSize メソッド
description: CPixel ComputeMipMapSize メソッドは、mipmap のテクスチャの割り当てに必要なメモリの量を決定します。
ms.assetid: f60883df-9200-4ae7-b130-21a6892e14be
keywords:
- ディスプレイ デバイスの ComputeMipMapSize メソッド
- ComputeMipMapSize メソッド ディスプレイ デバイス、CPixel インターフェイス
- CPixel インターフェイス ディスプレイ デバイス、ComputeMipMapSize メソッド
topic_type:
- apiref
api_name:
- CPixel.ComputeMipMapSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1b0b53d200d35fe0291f6c0b1d4f0471dc67ec46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537284"
---
# <a name="cpixelcomputemipmapsize-method"></a>CPixel::ComputeMipMapSize メソッド


**CPixel::ComputeMipMapSize**メソッドは、mipmap のテクスチャの割り当てに必要なメモリの量を決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
static UINT  ComputeMipMapSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cLevels,
   D3DFORMAT Format
);
```

<a name="parameters"></a>パラメーター
----------

*cpWidth* mipmap のテクスチャのピクセル単位の幅を指定します。

*cpHeight* mipmap のテクスチャのピクセル単位の高さを指定します。

*cLevels* mipmap のテクスチャのレベル数を指定します。

*形式*D3DFORMAT 列挙体の値を使用して、surface の形式を指定します。

<a name="return-value"></a>戻り値
------------

Mipmap のテクスチャのバイト単位のサイズを返します。

<a name="remarks"></a>注釈
-------

D3DFORMAT の詳細については、Microsoft DirectX SDK ドキュメントを参照してください。

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

 

 





