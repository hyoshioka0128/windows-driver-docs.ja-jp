---
title: DEVPROP_TYPE_SECURITY_DESCRIPTOR
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_SECURITY_DESCRIPTOR 識別子は、データ型が、可変長の自己相対 SECURITY_DESCRIPTOR に型指定されたセキュリティ記述子であることを示す基本データ型識別子を表します。
ms.assetid: e8eea343-adaa-41b8-9556-962b5e6903fb
keywords:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 089675e82ef432740f842184f9c6c12d8cb268db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580937"
---
# <a name="devproptypesecuritydescriptor"></a>DEVPROP_TYPE_SECURITY_DESCRIPTOR


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_SECURITY_DESCRIPTOR 識別子は、データ型が、可変長の自己相対 SECURITY_DESCRIPTOR に型指定されたセキュリティ記述子であることを示す基本データ型識別子を表します。

<a name="remarks"></a>コメント
-------

DEVPROP_TYPE_SECURITY_DESCRIPTOR は、データ型のプロパティの修飾子と組み合わせることはできません。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_SECURITY_DESCRIPTOR プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_SECURITY_DESCRIPTOR、パラメーターの設定、 *PropertyBuffer*可変長 SECURITY_DESCRIPTOR の構造を格納しているバッファーへのポインターへのパラメーターと設定、 *PropertyBufferSize*セキュリティ記述子構造体のバイト単位のサイズのパラメーター。

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

 

 





