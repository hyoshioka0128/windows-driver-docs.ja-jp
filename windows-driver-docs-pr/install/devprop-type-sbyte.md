---
title: DEVPROP_TYPE_SBYTE
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BYTE 識別子は、データ型が SBYTE 型指定の符号付き整数であることを示す基本データ型識別子を表します。
ms.assetid: d2c503aa-4427-4745-b3c2-57b6ebd0e93c
keywords:
- DEVPROP_TYPE_SBYTE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_SBYTE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c9f9af4a4eea1d661d99ab0593f1f5edb56aa891
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344310"
---
# <a name="devprop_type_sbyte"></a>DEVPROP_TYPE_SBYTE


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BYTE 識別子は、データ型が SBYTE 型指定の符号付き整数であることを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_SBYTE は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

データ型が DEVPROP_TYPE_BYTE プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数は、および関数のパラメーターを次のように設定します。

- 設定、 *PropertyType* DEVPROP_TYPE_BYTE、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つのバイト値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>バイト<strong>)</strong>します。

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

 

 





