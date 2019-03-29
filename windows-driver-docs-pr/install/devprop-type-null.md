---
title: DEVPROP_TYPE_NULL
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_NULL 識別子は、デバイス プロパティが存在することを示す特殊な基本データ型識別子を表します。 ただし、プロパティに値がないことに関連付けられているプロパティ。
ms.assetid: 0308206d-5664-4288-a761-ca72e533264c
keywords:
- DEVPROP_TYPE_NULL デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_NULL
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f5ba1bdac9df8044d91126266a65172fb7e2922d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570198"
---
# <a name="devproptypenull"></a>DEVPROP_TYPE_NULL


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_NULL 識別子は、デバイス プロパティが存在することを示す特殊な基本データ型識別子を表します。 ただし、プロパティに値がないことに関連付けられているプロパティ。

<a name="remarks"></a>コメント
-------

デバイスのプロパティ関数でこの基本プロパティ型識別子を使用すると、デバイスのプロパティに関連付けられている値を削除できます。

デバイスのプロパティ関数は、この基本データ型を返す場合は、プロパティが存在するが、プロパティには、それに関連付けられている値はありません。

DEVPROP_TYPE_NULL 識別子は、データ型のプロパティの修飾子と組み合わせることはできません[ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)または[ **DEVPROP_TYPEMOD_LIST**](devprop-typemod-list.md).

**このプロパティの種類の設定**

データ型が DEVPROP_TYPE_NULL プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** 関数のパラメーターとしてプロパティ関数とセットに従います。

-   設定、 *PropertyType* DEVPROP_TYPE_NULL、パラメーター、 *PropertyBuffer*パラメーターを**NULL**、および*PropertyBufferSize*パラメーターを 0 にします。

-   プロパティを設定する、必要に応じて、他の関数の入力パラメーターを設定します。

**この型のプロパティを取得します。**

呼び出しを**SetupDiGet * Xxx*** 値がないデバイス プロパティを取得しようとするプロパティ関数は成功し、設定、 \* *PropertyType* DEVPROP_TYPE_NULL パラメーター。

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

 

 





