---
title: CPixel ComputeMipVolumeOffset メソッド
description: CPixel ComputeMipVolumeOffset メソッドは、ミップマップ ボリューム テクスチャの subvolume オフセットを決定します。
ms.assetid: 4fb2f49a-2c1a-4b07-bbd3-76c4e345b243
keywords:
- ディスプレイ デバイスの ComputeMipVolumeOffset メソッド
- ComputeMipVolumeOffset メソッド ディスプレイ デバイス、CPixel インターフェイス
- CPixel インターフェイス ディスプレイ デバイス、ComputeMipVolumeOffset メソッド
topic_type:
- apiref
api_name:
- CPixel.ComputeMipVolumeOffset
api_location:
- pixel.hpp
api_type:
- COM
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f05d5372ef430cc729bfe3a4d4fea6cac0108750
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558918"
---
# <a name="cpixelcomputemipvolumeoffset-method"></a>CPixel::ComputeMipVolumeOffset メソッド


**CPixel::ComputeMipVolumeOffset**メソッドは、ミップマップ ボリューム テクスチャの subvolume オフセットを決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
static void  ComputeMipVolumeOffset(
   const D3DVOLUME_DESC *pDescTopLevel,
         UINT           iLevel,
         BYTE           *pBits,
   const D3DBOX         *pBox,
   const D3DLOCKED_BOX  *pLockedBoxData
);
```

<a name="parameters"></a>パラメーター
----------

*pDescTopLevel* 、D3DVOLUME へのポインター\_mipmap のテクスチャのボリュームの最上位のレベルを記述する DESC 構造体。

*iLevel*オフセットが決定される mipmap ボリュームのレベルを指定します。

*pBits* mipmap ボリューム テクスチャの最上位レベルの先頭へのポインターまたは**NULL**呼び出し元には、オフセットだけが必要な場合。

*pBox* 、subvolume を記述する D3DBOX 構造体へのポインターまたは**NULL**呼び出し元には、下位レベルの先頭のみが必要な場合。

*pLockedBoxData* 、D3DLOCKED へのポインター\_ボックス構造体を受け取るポインターまたはロックされているボリューム領域のオフセット。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

最上位レベル、および、subvolume サーフェスの説明、mipmap のボリュームのレベル、ポインターを指定**CPixel::ComputeMipVolumeOffset**でロックされているボックス領域に、ポインターやオフセットを返します、 **pBits**、D3DLOCKED のメンバー\_ボックス構造**pLockedBoxData**します。

D3DLOCKED の詳細については\_ボックスで、D3DVOLUME\_DESC、および D3DBOX は、Microsoft DirectX SDK ドキュメントを参照してください。

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

 

 





