---
title: DEVPROP_TYPE_UINT64
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が ULONG64 に型指定された符号なし整数であるかを示す基本データ型識別子を表します。
ms.assetid: a6dfb90d-0cae-4b63-bc27-57d7b0f6b897
keywords:
- DEVPROP_TYPE_UINT64 デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_UINT64
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3326d7a926b6598dfb70c1e681194cafe9320eed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553488"
---
# <a name="devproptypeuint64"></a>DEVPROP_TYPE_UINT64


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_INT64 識別子は、データ型が ULONG64 に型指定された符号なし整数であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_UINT64 は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

基本データ型は DEVPROP_TYPE_UINT64 プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

- 設定、 *PropertyType* DEVPROP_TYPE_UINT64、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの ULONG64 値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>ULONG64<strong>)</strong>します。

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

 

 





