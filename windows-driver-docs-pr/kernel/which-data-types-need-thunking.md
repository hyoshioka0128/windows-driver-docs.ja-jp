---
title: サンキングが必要なデータ型
description: サンキングが必要なデータ型
ms.assetid: af1d7986-7bf2-4587-b487-91658e7a3b19
keywords:
- サンクの WDK
- WOW64 サンク レイヤー WDK
- 32 ビットの I/O をサポートして WDK 64 ビット、サンキング
- データ型の WDK 64 ビット
- ポインターの精度を WDK の 64 ビット
- 固定精度のデータ型を WDK の 64 ビット
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4f6ca86749a487a1d7bfd04abffa81793ffab29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383198"
---
# <a name="which-data-types-need-thunking"></a>サンキングが必要なデータ型





次の表には、同等の thunked と共に、サンクを必要とする共通のデータ型が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>(サンク) 前に、のポインターの精度のデータ型</th>
<th>等価の 32 ビットの固定精度データ型 (サンク) した後</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ハンドル</p></td>
<td><p>VOID * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>INT_PTR</p></td>
<td><p>INT32</p></td>
</tr>
<tr class="odd">
<td><p>LONG_PTR</p></td>
<td><p>LONG32</p></td>
</tr>
<tr class="even">
<td><p>LPARAM</p></td>
<td><p>LONG32</p></td>
</tr>
<tr class="odd">
<td><p>PCHAR</p></td>
<td><p>Char * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>PDWORD</p></td>
<td><p>DWORD * POINTER_32</p></td>
</tr>
<tr class="odd">
<td><p>PHANDLE</p></td>
<td><p>VOID * * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>PULONG</p></td>
<td><p>ULONG * POINTER_32</p></td>
</tr>
<tr class="odd">
<td><p>PVOID</p></td>
<td><p>VOID * POINTER_32</p></td>
</tr>
<tr class="even">
<td><p>PWORD</p></td>
<td><p>WORD * POINTER_32</p></td>
</tr>
<tr class="odd">
<td><p>SIZE_T</p></td>
<td><p>INT32</p></td>
</tr>
<tr class="even">
<td><p>ULONG_PTR</p></td>
<td><p>ULONG32</p></td>
</tr>
<tr class="odd">
<td><p>UNICODE_STRING</p></td>
<td><p>UNICODE_STRING32</p></td>
</tr>
</tbody>
</table>

 

 

 




