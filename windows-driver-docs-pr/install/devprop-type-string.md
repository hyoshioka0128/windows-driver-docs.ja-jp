---
title: DEVPROP_TYPE_STRING
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_STRING プロパティの型は、データ型が NULL で終わる Unicode 文字列であることを示します基本データ型識別子を表します。
ms.assetid: b578fa1f-b55d-4ad2-bdc4-a796b5d7b811
keywords:
- DEVPROP_TYPE_STRING デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_STRING
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4c835ce41382e712c5c652d823e0f9f5f3bfb2c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539490"
---
# <a name="devproptypestring"></a>DEVPROP_TYPE_STRING


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_STRING プロパティの型は、データ型が NULL で終わる Unicode 文字列であることを示します基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_STRING は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_LIST** ](devprop-typemod-list.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_STRING プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数、関数の入力パラメーターを次のように設定します。

-   設定、 *PropertyType* DEVPROP_TYPE_STRING、パラメーターの設定、 *PropertyBuffer*パラメーターを NULL で終わる Unicode 文字列を含むバッファーへのポインターを設定し、 *PropertyBufferSize*パラメーターを NULL 終端文字を含む文字列のバイト単位のサイズ。

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

 

 





