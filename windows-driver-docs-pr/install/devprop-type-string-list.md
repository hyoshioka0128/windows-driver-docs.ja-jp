---
title: DEVPROP_TYPE_STRING_LIST
description: Windows Vista および以降のバージョンの Windows では、DEVPROP_TYPE_STRING_LIST プロパティの型がデータの種類があるかを示す基本データ型識別子を表す、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-Unicode 文字列の型指定されたリスト。
ms.assetid: 91cfba02-cdd4-4918-8fc1-7e7793058074
keywords:
- DEVPROP_TYPE_STRING_LIST デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_STRING_LIST
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ee4fe69ccdd80dcc22a8ce0a09f6fb5ef44a3811
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580816"
---
# <a name="devproptypestringlist"></a>DEVPROP_TYPE_STRING_LIST


Windows Vista および以降のバージョンの Windows では、DEVPROP_TYPE_STRING_LIST プロパティの型がデータの種類があるかを示す基本データ型識別子を表す、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-Unicode 文字列の型指定されたリスト。

<a name="remarks"></a>コメント
-------

DEVPROP_TYPE_STRING_LIST は、データ型のプロパティの修飾子と組み合わせることはできません。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_STRING_LIST プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_STRING_LIST、パラメーターの設定、 *PropertyBuffer*パラメーターを格納するバッファーへのポインターを[REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)の一覧Unicode 文字列を設定し、 *PropertyBufferSize*最終的な一覧に NULL 終端文字を含め、リストのバイト単位のサイズのパラメーター。

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

 

 





