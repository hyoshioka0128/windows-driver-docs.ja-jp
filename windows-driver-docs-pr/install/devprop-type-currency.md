---
title: DEVPROP_TYPE_CURRENCY
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_CURRENCY 識別子は、データ型が通貨に型指定された値であるかを示す基本データ型識別子を表します。
ms.assetid: e79d4351-79a0-4e7a-9290-dd02d317a958
keywords:
- DEVPROP_TYPE_CURRENCY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_CURRENCY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 54a92b68383cd388c92989c654f14c9a4500f687
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360627"
---
# <a name="devproptypecurrency"></a>DEVPROP_TYPE_CURRENCY


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_CURRENCY 識別子は、データ型が通貨に型指定された値であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_CURRENCY は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>この型のプロパティを設定

基本データ型は DEVPROP_TYPE_CURRENCY プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_CURRENCY、パラメーターの設定、 *PropertyBuffer*通貨の値を格納しているバッファーへのポインターにパラメーターを設定し、 *PropertyBufferSize*パラメーター`sizeof(CURRENCY)`します。

-   プロパティを設定する、必要に応じて、他の関数の入力パラメーターを設定します。

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

 

 





