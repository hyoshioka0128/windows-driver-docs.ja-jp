---
title: WIA\_IP\_サポートされている\_PATCH\_コード\_型
description: WIA ミニドライバーは、WIA を使用して\_IP\_サポートされている\_PATCH\_コード\_型のプロパティを修正プログラム コード リーダーでは、(認識) がサポートされているすべての修正プログラム コードの種類を一覧表示します。
ms.assetid: DA55BFFD-64E9-4D96-AB04-F2112E1F117B
keywords:
- WIA_IPS_SUPPORTED_PATCH_CODE_TYPES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_SUPPORTED_PATCH_CODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c47b9810313db00796afbfacca7d5a353d1838d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343836"
---
# <a name="wiaipssupportedpatchcodetypes"></a>WIA\_IP\_サポートされている\_PATCH\_コード\_型


WIA ミニドライバーを使用して、 **WIA\_IP\_サポートされている\_PATCH\_コード\_型**プロパティ (認識) 更新プログラムでサポートされているすべての修正プログラム コードの種類を一覧表示するにはコード リーダー。 サポートされているバーコードのタイプは、VT で報告される\_として複数のエントリを含む 1 つの値のベクターの配列。




プロパティの種類:VT\_I4 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE (1 つの 'array'/値のベクトル)

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_サポートされている\_PATCH\_コード\_型**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PATCH_CODE_1</p></td>
<td><p>修正プログラム コード 1</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_2</p></td>
<td><p>修正プログラム コード 2</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_3</p></td>
<td><p>コードの更新プログラム 3</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_4</p></td>
<td><p>コードの更新プログラム 4</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_6</p></td>
<td><p>コードの更新プログラム 6</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_T</p></td>
<td><p>修正プログラム コード T</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_CUSTOM_BASE + N</p></td>
<td><p>WIA_PATCH_CODE_CUSTOM_BASE は、WIA ミニドライバーは追加するすべての修正プログラムのカスタム コード値にオフセットです。 N は、正の整数です。</p></td>
</tr>
</tbody>
</table>

 

WIA ミニドライバーは、WIA として定義されている追加のカスタム値でこのリストを拡張することができます\_PATCH\_コード\_カスタム\_基本 + N、N は正の整数。

このプロパティは、修正プログラム コード リーダーのすべての項目に必要です。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





