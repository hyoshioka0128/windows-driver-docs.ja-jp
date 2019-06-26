---
title: プロパティ値の要件
description: プロパティ値の要件
ms.assetid: 05512f3d-fe64-4de0-848c-c983d883fc60
keywords:
- デバイス プロパティ WDK デバイス インストールでは、プロパティ値の要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 719a8ce9d66c84a73f9ad2fb9e7e9bbafc6172a3
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393474"
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
<td align="left"><p>固定長<a href="https://docs.microsoft.com/previous-versions/ff537793(v=vs.85)" data-raw-source="[&lt;strong&gt;base-data-type&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff537793(v=vs.85))"><strong>基本データ型</strong></a>値</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、基本データ型のバイト数である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>固定長の基本データ型値の配列</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、0 個以上の基本データ型の値の配列のバイト数である必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>A <a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor)"> <strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR</strong> </a>データ型の値</p></td>
<td align="left"><p>指定されたデータの指定したサイズは、可変長の自己相対 SECURITY_DESCRIPTOR 構造体のバイト数である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>A <a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string)"> <strong>DEVPROP_TYPE_STRING</strong> </a>データ型の値を<a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor-string" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor-string)"> <strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING</strong> </a>データ型の値、または、 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string-indirect" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_INDIRECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string-indirect)"> <strong>DEVPROP_TYPE_STRING_INDIRECT</strong> </a>データ型の値</p></td>
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

 

 

 





