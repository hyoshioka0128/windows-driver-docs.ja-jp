---
title: プロパティ値の要件
description: プロパティ値の要件
ms.assetid: 05512f3d-fe64-4de0-848c-c983d883fc60
keywords:
- デバイス プロパティ WDK デバイス インストールでは、プロパティ値の要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 148c94e06691f4153b56c3d93bca006ddaff6953
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391980"
---
# <a name="property-value-requirements"></a>プロパティ値の要件


Windows では、次の表に記載されているデバイス プロパティの値のサイズ要件を強制します。 Windows は、デバイスのプロパティの値は、これらの値のサイズ要件に準拠している場合にのみデバイスのプロパティ値を設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プロパティのデータ型</th>
<th align="left">プロパティ値のサイズ要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>固定長<a href="https://msdn.microsoft.com/library/windows/hardware/ff537793" data-raw-source="[&lt;strong&gt;base-data-type&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537793)"><strong>基本データ型</strong></a>値</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、基本データ型のバイト数である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>固定長の基本データ型値の配列</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、0 個以上の基本データ型の値の配列のバイト数である必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>A <a href="https://msdn.microsoft.com/library/windows/hardware/ff543608" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543608)"> <strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR</strong> </a>データ型の値</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、可変長の自己相対 SECURITY_DESCRIPTOR 構造体のバイト数である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>A <a href="https://msdn.microsoft.com/library/windows/hardware/ff543612" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543612)"> <strong>DEVPROP_TYPE_STRING</strong> </a>データ型の値を<a href="https://msdn.microsoft.com/library/windows/hardware/ff543609" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543609)"> <strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING</strong> </a>データ型の値、または、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff543613" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_INDIRECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543613)"> <strong>DEVPROP_TYPE_STRING_INDIRECT</strong> </a>データ型の値</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、Unicode のバイト数である必要があります<a href="https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types" data-raw-source="[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)">REG_SZ</a> NULL ターミネータを含む文字列。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEVPROP_TYPE_STRING に型指定された文字列のリスト、DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING に型指定された文字列、または DEVPROP_TYPE_STRING_LIST データの一覧の値を入力します。</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、最終的な終端の NULL 終了文字列のリストを含む文字列の Unicode REG_MULTLI_SZ リストのバイト数である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>すべてのプロパティ値</p></td>
<td align="left"><p>このテーブルの他の行に記載されているプロパティの値のサイズ要件、に加えてプロパティ値のバイト単位の最大サイズは UNICODE_STRING_MAX_BYTES です。</p></td>
</tr>
</tbody>
</table>

 

 

 





