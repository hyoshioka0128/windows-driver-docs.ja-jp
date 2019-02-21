---
title: DEVPROP_TYPE_DATE
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DATE プロパティの型は、データ型が、1899 年 12 月 31 日からの日数の数を指定する DOUBLE 型の値を示す基本データ型識別子を表します。
ms.assetid: 0314e7da-d1da-4989-b2cd-90a51c3c8938
keywords:
- DEVPROP_TYPE_DATE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_DATE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 55d17d6ca3d644ff7f57683d18a2b3ec23fe9f41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560466"
---
# <a name="devproptypedate"></a>DEVPROP_TYPE_DATE


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_DATE プロパティの型は、データ型が、1899 年 12 月 31 日からの日数の数を指定する DOUBLE 型の値を示す基本データ型識別子を表します。 たとえば、1900 年 1 月 1 日には 1.0 です。1900 年 1 月 2 日は 2.0 です。などなど。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_DATE は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_DATE プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_DATE、パラメーターの設定、 *PropertyBuffer* 、日付の値を格納しているバッファーへのポインターにパラメーターを設定し、 *PropertyBufferSize*パラメーター`sizeof(DATE)`します。

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

 

 





