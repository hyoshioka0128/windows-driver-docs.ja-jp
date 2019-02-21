---
title: DEVPROP_TYPE_BINARY
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BINARY 識別子は、データ型が符号なしの値をバイトに型指定された配列であるかを示す基本データ型識別子を表します。
ms.assetid: ee20f0f1-fff9-41a9-a880-f8f577320e41
keywords:
- DEVPROP_TYPE_BINARY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_BINARY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aca3498dc91865e6bf8a8d2a5c0114879b494eb0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528421"
---
# <a name="devproptypebinary"></a>DEVPROP_TYPE_BINARY


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_BINARY 識別子は、データ型が符号なしの値をバイトに型指定された配列であるかを示す基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_BINARY プロパティの型は、データ型のプロパティの修飾子と組み合わせることはできません。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_BINARY プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_BINARY、パラメーターの設定、 *PropertyBuffer*バイト値、およびセットの配列を格納しているバッファーへのポインターへのパラメーター、 *PropertyBufferSize*パラメーター バッファーのバイト単位のサイズにします。

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

 

 





