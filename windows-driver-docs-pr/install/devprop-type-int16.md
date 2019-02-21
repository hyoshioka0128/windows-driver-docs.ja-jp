---
title: DEVPROP_TYPE_INT16
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT16 識別子は、データ型が SHORT 型の符号付き整数であることを示す基本データ型識別子を表します。
ms.assetid: a126a7c2-744e-4eaf-9b3d-45bd4286de73
keywords:
- DEVPROP_TYPE_INT16 デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_INT16
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: df7761f863def61a267639df0d5fe7fd39912293
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538785"
---
# <a name="devproptypeint16"></a>DEVPROP_TYPE_INT16


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT16 識別子は、データ型が SHORT 型の符号付き整数であることを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_SHORT は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

基本データ型は DEVPROP_TYPE_INT16 プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

- 設定、 *PropertyType* DEVPROP_TYPE_INT16、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの短い値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>短い<strong>)</strong>します。

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

 

 





