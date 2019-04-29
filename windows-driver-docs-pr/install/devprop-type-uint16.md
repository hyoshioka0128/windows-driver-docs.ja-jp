---
title: DEVPROP_TYPE_UINT16
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_UINT16 識別子は、データ型が USHORT に型指定された符号なし整数であるかを示す基本データ型識別子を表します。
ms.assetid: 8df7fc86-bad3-44cd-9ff1-552a69dd378b
keywords:
- DEVPROP_TYPE_UINT16 デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_UINT16
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 886ee0ff92461e4b7f70ea6c35a11c0db5541fe2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331280"
---
# <a name="devproptypeuint16"></a>DEVPROP_TYPE_UINT16


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_UINT16 識別子は、データ型が USHORT に型指定された符号なし整数であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_UINT16 は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

**このプロパティの種類の設定**

基本データ型は DEVPROP_TYPE_UINT16 プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

- 設定、 *PropertyType* DEVPROP_TYPE_UINT16、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの USHORT 値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>USHORT<strong>)</strong>します。

- プロパティを設定する、必要に応じて、他の関数の入力パラメーターを設定します。

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

 

 





