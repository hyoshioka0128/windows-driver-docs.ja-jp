---
title: DEVPROP_TYPE_BOOLEAN
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BOOLEAN プロパティの型は、データ型が DEVPROP_BOOLEAN に型指定されたブール値であるかを示す基本データ型識別子を表します。
ms.assetid: f0e960b7-be71-4117-b978-5877e5bf771f
keywords:
- DEVPROP_TYPE_BOOLEAN デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_BOOLEAN
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 645593588841c0d10157cacc7e64f4f5328846b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327480"
---
# <a name="devproptypeboolean"></a>DEVPROP_TYPE_BOOLEAN


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BOOLEAN プロパティの型は、データ型が DEVPROP_BOOLEAN に型指定されたブール値であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_BOOLEAN データ型および有効なブール値は、次のように定義されます。

``` syntax
typedef CHAR DEVPROP_BOOLEAN, *PDEVPROP_BOOLEAN;
#define DEVPROP_TRUE  ((DEVPROP_BOOLEAN)-1)
#define DEVPROP_FALSE ((DEVPROP_BOOLEAN) 0)
```

DEVPROP_TYPE_BOOLEAN は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_BOOLEAN プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_BOOLEAN、パラメーターの設定、 *PropertyBuffer* DEVPROP_FALSE または DEVPROP_TRUE の値を格納しているバッファーへのポインターにパラメーターを設定し、 *PropertyBufferSize*パラメーター`sizeof(DEVPROP_BOOLEAN)`します。

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

 

 





