---
title: DEVPROP_TYPEMOD_ARRAY
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPEMOD_ARRAY 識別子は配列を表すデータ型のプロパティの識別子を作成する基本データ型識別子を組み合わせてプロパティ データ型修飾子を表します。基本データ型の値。
ms.assetid: 33f12b66-c81a-451b-851a-b58a34a8fe9e
keywords:
- DEVPROP_TYPEMOD_ARRAY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPEMOD_ARRAY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9c469e72b9b44da2a0f9f6506cd9251670d21c15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331270"
---
# <a name="devproptypemodarray"></a>DEVPROP_TYPEMOD_ARRAY


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPEMOD_ARRAY 識別子はで結合できますプロパティ データ型修飾子を表します、 [**基本データ型識別子**](https://msdn.microsoft.com/library/windows/hardware/ff537793)を作成する。基本データ型の値の配列を表すデータ型のプロパティの識別子です。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPEMOD_ARRAY 識別子は、固定長の基本データ型識別子とのみ組み合わせることができます ([**DEVPROPTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff543546)値) データに関連付けられています。 DEVPROP_TYPEMOD_ARRAY 識別子は組み合わせることができない[ **DEVPROP_TYPE_EMPTY**](devprop-type-empty.md)、 [ **DEVPROP_TYPE_NULL**](devprop-type-null.md)、またはのいずれか、可変長の基本データ型識別子。

基本データ型の値の配列を表すデータ型のプロパティの識別子を作成するには、DEVPROP_TYPEMOD_ARRAY と対応する DEVPROP_TYPE_ 間でビットごとの OR を実行*Xxx*識別子。 たとえば、符号なしバイトの配列を指定するには、次のビットごとの OR を実行します。(DEVPROP_TYPEMOD_ARRAY | [**DEVPROP_TYPE_BYTE**](devprop-type-byte.md)).

基本データ型の値の配列のバイト単位のサイズは、配列のバイト単位のサイズです。

表すデータ型のプロパティの識別子を作成する方法については、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)リスト、NULL で終わる Unicode 文字列の次を参照してください[ **DEVPROP_TYPEMOD_LIST** 。](devprop-typemod-list.md).

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


[**DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)

[**DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md)

 

 






