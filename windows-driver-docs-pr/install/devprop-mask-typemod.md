---
title: DEVPROP_MASK_TYPEMOD
description: Windows Vista および以降のバージョンの Windows では、データ型のプロパティの識別子から DEVPROP_TYPEMOD_Xxx プロパティ データ型の修飾子を抽出するデータ型のプロパティの識別子を持つ DEVPROP_MASK_TYPEMOD マスク ビットごとの AND で結合できます。
ms.assetid: 9ed153d7-dd37-4978-9e03-44efac2ab97a
keywords:
- DEVPROP_MASK_TYPEMOD デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_MASK_TYPEMOD
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 209ed77f0fbe7dc6f9193a5a4a64e3caa3dfe465
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327427"
---
# <a name="devpropmasktypemod"></a>DEVPROP_MASK_TYPEMOD


Windows Vista および以降のバージョンの Windows では、DEVPROP_MASK_TYPEMOD マスクでビットごとの AND で結合できます、[プロパティ データ型識別子](https://msdn.microsoft.com/library/windows/hardware/ff541476)、DEVPROP_TYPEMOD_ を抽出する*Xxx*  [**プロパティ データ型の修飾子**](https://msdn.microsoft.com/library/windows/hardware/ff549770)データ型のプロパティの識別子から。

<a name="remarks"></a>注釈
-------

このマスクは、基本データ型識別子、データ型のプロパティの修飾子、またはデータ型のプロパティの識別子として使用できません。

抽出する方法については、 [**基本データ型識別子**](https://msdn.microsoft.com/library/windows/hardware/ff537793)からデータ型のプロパティの識別子では、次を参照してください[ **DEVPROP_MASK_TYPE** 。](devprop-mask-type.md).

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVPROP_MASK_TYPE**](devprop-mask-type.md)

 

 






