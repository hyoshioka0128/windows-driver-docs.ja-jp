---
title: DEVPROP_TYPE_FLOAT
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が float 型に型指定された IEEE 浮動小数点数を示す基本データ型識別子を表します。
ms.assetid: b83a0510-674e-4141-9d3f-25efcb08aea0
keywords:
- DEVPROP_TYPE_FLOAT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_FLOAT
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4ff72b81f72c49cbe699e3d9a39ceb7e7e2fae0c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558296"
---
# <a name="devproptypefloat"></a>DEVPROP_TYPE_FLOAT


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が float 型に型指定された IEEE 浮動小数点数を示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_FLOAT は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

基本データ型は DEVPROP_TYPE_FLOAT プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数、関数の入力パラメーターを次のように設定します。

-   設定、 *PropertyType* DEVPROP_TYPE_FLOAT、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの浮動小数点値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーター`sizeof(FLOAT)`します。

-   プロパティを設定する、必要に応じて、他の関数の入力パラメーターを設定します。

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

 

 





