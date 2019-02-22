---
title: DEVPROP_TYPE_DEVPROPTYPE
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DEVPROPTYPE 識別子は、データ型が DEVPROPTYPE に型指定された値であることを示す基本データ型識別子を表します。
ms.assetid: d50a26d4-0af5-4cc5-aaa4-8587b64fc1a8
keywords:
- DEVPROP_TYPE_DEVPROPTYPE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DEVPROPTYPE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6ba4d0c9147a772a546a4a28a25ff018a1832a6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535572"
---
# <a name="devproptypedevproptype"></a>DEVPROP_TYPE_DEVPROPTYPE


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DEVPROPTYPE 識別子は、データ型が DEVPROPTYPE に型指定された値であることを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_DEVPROPTYPE プロパティの型は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_DEVPROPTYPE プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数、関数の入力パラメーターを次のように設定します。

-   設定、 *PropertyType* DEVPROP_TYPE_DEVPROPTYPE、パラメーターの設定、 *PropertyBuffer* DEVPROPTYPE 値を格納しているバッファーへのポインターにパラメーターを設定し、 *PropertyBufferSize*パラメーター`sizeof(DEVPROPTYPE)`します。

-   プロパティを設定する適切な関数の残りのパラメーターを設定します。

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

 

 





