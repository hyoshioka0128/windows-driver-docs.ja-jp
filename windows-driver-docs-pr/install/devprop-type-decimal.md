---
title: DEVPROP_TYPE_DECIMAL
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が 10 進数に型指定された値であるかを示す基本データ型識別子を表します。
ms.assetid: 3aacffd6-3259-489b-992d-e2771858c1e6
keywords:
- DEVPROP_TYPE_DECIMAL デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DECIMAL
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fac40baf3506a84ed1c7a5ca212a67f86eb0e70a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383682"
---
# <a name="devproptypedecimal"></a>DEVPROP_TYPE_DECIMAL


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が 10 進数に型指定された値であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_DECIMAL は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

データ型が DEVPROP_TYPE_DECIMAL プロパティを設定する呼び出しの対応する SetupDiSet*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_DECIMAL、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの 10 進値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーター`sizeof(DECIMAL)`します。

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

 

 





