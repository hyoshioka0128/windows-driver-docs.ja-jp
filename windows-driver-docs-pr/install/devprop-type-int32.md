---
title: DEVPROP_TYPE_INT32
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT32 識別子は、データ型が LONG 型の符号付き整数であるかを示す基本データ型識別子を表します。
ms.assetid: 55a26644-1779-4330-8a45-52b06b634544
keywords:
- DEVPROP_TYPE_INT32 デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_INT32
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7a669b152c2a3570e9eee86d817a7529b09aa2a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530343"
---
# <a name="devproptypeint32"></a>DEVPROP_TYPE_INT32


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT32 識別子は、データ型が LONG 型の符号付き整数であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_INT32 は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

基本データ型は DEVPROP_TYPE_INT32 プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数、関数の入力パラメーターを次のように設定します。

- 設定、 *PropertyType* DEVPROP_TYPE_INT32、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの long 型の値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>長い<strong>)</strong>します。

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

 

 





