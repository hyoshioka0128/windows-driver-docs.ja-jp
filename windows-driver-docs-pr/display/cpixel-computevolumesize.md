---
title: CPixel ComputeVolumeSize メソッド
description: CPixel ComputeVolumeSize メソッドは、ボリュームを割り当てるに必要なメモリの量を決定します。
ms.assetid: 85e00793-8c30-41a4-91b0-9f0503a6ce09
keywords:
- ディスプレイ デバイスの ComputeVolumeSize メソッド
- ComputeVolumeSize メソッド ディスプレイ デバイス、CPixel インターフェイス
- CPixel インターフェイス ディスプレイ デバイス、ComputeVolumeSize メソッド
topic_type:
- apiref
api_name:
- CPixel.ComputeVolumeSize
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e217c5fa904d17115a7fcc52181b9dfccacf66c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389994"
---
# <a name="cpixelcomputevolumesize-method"></a>CPixel::ComputeVolumeSize メソッド


**CPixel::ComputeVolumeSize**メソッドは、ボリュームを割り当てるに必要なメモリの量を決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
static UINT ComputeVolumeSize(
   UINT      cpWidth,
   UINT      cpHeight,
   UINT      cpDepth,
   D3DFORMAT Format
);
```

<a name="parameters"></a>パラメーター
----------

*cpWidth*ボリュームのピクセル単位の幅を指定します。

*cpHeight*ボリュームのピクセル単位の高さを指定します。

*cpDepth*ボリュームのピクセルの深さを指定します。

*形式*D3DFORMAT 列挙体の値を使用して、surface の形式を指定します。

<a name="return-value"></a>戻り値
------------

ボリュームのバイト単位のサイズを返します。

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

 

 





