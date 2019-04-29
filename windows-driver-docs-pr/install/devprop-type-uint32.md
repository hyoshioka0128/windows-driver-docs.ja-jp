---
title: DEVPROP_TYPE_UINT32
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_UINT32 識別子は、データ型が ULONG 型指定の符号なし整数であるかを示す基本データ型識別子を表します。
ms.assetid: 671474dd-66be-4c35-8f1a-273f61c6343c
keywords:
- DEVPROP_TYPE_UINT32 デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_UINT32
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c3d8ab2909ed84c4bbb438712c3efb837421489a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331275"
---
# <a name="devproptypeuint32"></a>DEVPROP_TYPE_UINT32


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_UINT32 識別子は、データ型が ULONG 型指定の符号なし整数であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_UINT32 は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

基本データ型は DEVPROP_TYPE_UINT32 プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

- 設定、 *PropertyType* DEVPROP_TYPE_UINT32、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの ULONG 値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>ULONG<strong>)</strong>します。

- プロパティを設定する、必要に応じて、他の関数の入力パラメーターを設定します。

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
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





