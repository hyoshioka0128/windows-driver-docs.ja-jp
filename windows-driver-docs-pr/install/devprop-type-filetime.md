---
title: DEVPROP_TYPE_FILETIME
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_FILETIME プロパティの型は、データ型が FILETIME に型指定された値であるかを示す基本データ型識別子を表します。
ms.assetid: e81585ae-ee47-456b-b29b-24217fab5f9a
keywords:
- DEVPROP_TYPE_FILETIME デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_FILETIME
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b18b9cb7afb3f2bda4a519dbe26c5f49bddd3349
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553985"
---
# <a name="devproptypefiletime"></a>DEVPROP_TYPE_FILETIME


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_FILETIME プロパティの型は、データ型が FILETIME に型指定された値であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

すべての時間値は、世界協定時刻 (UTC) 単位で表すことをお勧めします。

DEVPROP_TYPE_FILETIME は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_FILETIME プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_DATE、パラメーターの設定、 *PropertyBuffer* 、FILETIME 構造体を格納しているバッファーへのポインターにパラメーターを設定し、 *PropertyBufferSize*パラメーター`sizeof(FILETIME)`します。

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

 

 





