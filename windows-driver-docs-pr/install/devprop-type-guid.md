---
title: DEVPROP_TYPE_GUID
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_GUID 識別子は、データ型が、GUID に型指定されたグローバル一意識別子 (GUID) を示す基本データ型識別子を表します。
ms.assetid: 77080860-c2b3-4c7c-8ab8-e0b02582ffbb
keywords:
- DEVPROP_TYPE_GUID デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_GUID
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 07c3280dc99818f75223af4d6ef7415093b84933
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578747"
---
# <a name="devproptypeguid"></a>DEVPROP_TYPE_GUID


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_GUID 識別子は、データ型が、GUID に型指定されたグローバル一意識別子 (GUID) を示す基本データ型識別子を表します。

<a name="remarks"></a>コメント
-------

DEVPROP_TYPE_GUID は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_GUID プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_GUID、パラメーターの設定、 *PropertyBuffer*パラメーターの GUID 値を格納しているバッファーへのポインターを設定し、 *PropertyBufferSize*パラメーター`sizeof(GUID)`します。

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

 

 





