---
title: DEVPROP_TYPE_DEVPROPKEY
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DEVPROPKEY 識別子は、データ型が DEVPROPKEY に型指定されたデバイス プロパティのキーであることを示す基本データ型識別子を表します。
ms.assetid: 4b0f0f33-9a9e-498a-b2f3-e215bac68dd9
keywords:
- DEVPROP_TYPE_DEVPROPKEY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DEVPROPKEY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 348cab367d2199aeefcc7b6459a97a673d0f61a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357889"
---
# <a name="devproptypedevpropkey"></a>DEVPROP_TYPE_DEVPROPKEY


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DEVPROPKEY 識別子は、データ型が DEVPROPKEY に型指定されたデバイス プロパティのキーであることを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_DEVPROPKEY プロパティの型は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_DEVPROPKEY プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_DEVPROPKEY、パラメーターの設定、 *PropertyBuffer* DEVPROPKEY 構造体を格納しているバッファーへのポインターにパラメーターを設定し、 *PropertyBufferSize*パラメーター`sizeof(DEVPROPKEY)`します。

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

 

 





