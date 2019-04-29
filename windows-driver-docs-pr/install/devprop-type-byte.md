---
title: DEVPROP_TYPE_BYTE
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BYTE 識別子は、データ型がバイトに型指定された符号なし整数であることを示す基本データ型識別子を表します。
ms.assetid: cda681f0-948d-4534-bf56-2ad9dd8a845c
keywords:
- DEVPROP_TYPE_BYTE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_BYTE
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f51f32856d6c6c646ab4a5c0dcd96bb9d03c4fee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327438"
---
# <a name="devproptypebyte"></a>DEVPROP_TYPE_BYTE


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BYTE 識別子は、データ型がバイトに型指定された符号なし整数であることを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_BYTE は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

データ型が DEVPROP_TYPE_BYTE プロパティを設定する呼び出しの対応する SetupDiSet*Xxx*プロパティ関数、関数の入力パラメーターを次のように設定します。

-   設定、 *PropertyType* DEVPROP_TYPE_BYTE、パラメーターの設定、 *PropertyBuffer*パラメーターを少なくとも 1 つのバイト値を含めることができ、設定するバッファーへのポインター、 *PropertyBufferSize*パラメーター`sizeof(BYTE)`します。

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

 

 





