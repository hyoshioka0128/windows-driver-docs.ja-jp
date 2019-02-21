---
title: CPixel ComputeMipVolumeSize メソッド
description: CPixel ComputeMipVolumeSize メソッドは、mipmap のテクスチャのボリュームを割り当てるに必要なメモリの量を決定します。
ms.assetid: f759421a-a41e-4705-8a18-124f7efb059b
keywords:
- ディスプレイ デバイスの ComputeMipVolumeSize メソッド
- ComputeMipVolumeSize メソッド ディスプレイ デバイス、CPixel インターフェイス
- CPixel インターフェイス ディスプレイ デバイス、ComputeMipVolumeSize メソッド
topic_type:
- apiref
api_name:
- CPixel.ComputeMipVolumeSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c308fcb3462440e902b071e73e608bc7c6ea7370
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560565"
---
# <a name="cpixelcomputemipvolumesize-method"></a>CPixel::ComputeMipVolumeSize メソッド


**CPixel::ComputeMipVolumeSize**メソッド mipmap テクスチャのボリュームを割り当てるに必要なメモリの量を決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
static UINT ComputeMipVolumeSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cpDepth,
   UINT      cLevels,
   D3DFORMAT Format
);
```

<a name="parameters"></a>パラメーター
----------

*cpWidth* mipmap ボリュームのピクセル単位の幅を指定します。

*cpHeight* mipmap ボリュームのピクセル単位の高さを指定します。

*cpDepth* mipmap ボリュームのピクセルの深さを指定します。

*cLevels* mipmap ボリューム テクスチャのレベルの数を指定します。

*形式*D3DFORMAT 列挙体の値を使用して、surface の形式を指定します。

<a name="return-value"></a>戻り値
------------

Mipmap のボリュームのバイト単位のサイズを返します。

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

 

 





