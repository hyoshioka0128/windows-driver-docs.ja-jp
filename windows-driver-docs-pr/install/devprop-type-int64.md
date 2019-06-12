---
title: DEVPROP_TYPE_INT64
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が LONG64 に型指定の符号付き整数であるかを示す基本データ型識別子を表します。
ms.assetid: a7ead755-385e-4efe-832d-885fff10e42f
keywords:
- DEVPROP_TYPE_INT64 デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_INT64
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0cf61b28ebecf8f45b0feb969fa36852df08a849
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528026"
---
# <a name="devproptypeint64"></a>DEVPROP_TYPE_INT64


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が LONG64 に型指定の符号付き整数であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_INT64 は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

基本データ型は DEVPROP_TYPE_INT64 プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

- 設定、 *PropertyType* DEVPROP_TYPE_INT64、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの LONG64 値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>LONG64<strong>)</strong>します。

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

 

 





