---
title: DEVPROP_TYPE_DOUBLE
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DOUBLE 識別子は、データ型が二重に型指定された IEEE 浮動小数点数を示す基本データ型識別子を表します。
ms.assetid: c04f8538-ce0d-4eaf-a4d5-86968dbc18fd
keywords:
- DEVPROP_TYPE_DOUBLE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DOUBLE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d231f8c14774d5f4c3e9af6839247504b368ec5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339657"
---
# <a name="devproptypedouble"></a>DEVPROP_TYPE_DOUBLE


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DOUBLE 識別子は、データ型が二重に型指定された IEEE 浮動小数点数を示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_DOUBLE は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_DOUBLE プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_DOUBLE、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの ULONG 値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーター`sizeof(DOUBLE)`します。

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

 

 





