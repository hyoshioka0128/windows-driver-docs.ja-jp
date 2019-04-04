---
title: ZwRegistryOpen ルール (storport)
description: このルールは、ZwOpenKey を使用して開いたレジストリ キーを識別するハンドルはその他の ZwXxx ルーチンで正しく使用される、その後ことを確認します。
ms.assetid: E423616B-C990-4D26-ABB4-6061BF3B6A21
ms.date: 05/21/2018
keywords:
- ZwRegistryOpen ルール (storport)
topic_type:
- apiref
api_name:
- ZwRegistryOpen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97961ad3554ff0236738beb392232e2a4d90a9f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553101"
---
# <a name="zwregistryopen-rule-storport"></a>ZwRegistryOpen ルール (storport)


このルールを使用して、レジストリ キーを識別するハンドルを開いたことを確認します。 **ZwOpenKey**他 ZwXxx ルーチンで正しく使用されて、その後です。 ルーチン**ZwEnumerateKey**、 **ZwEnumerateValueKey**、 **ZwFlushKey**、 **ZwQueryKey**、 **ZwQueryValueKey**、 **ZwSetValueKey**、 **ZwClose**、および**ZwDeleteKey**が開いていないハンドルを呼び出さないする必要があります。 返す前にハンドルを閉じてもする必要があります。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ZwRegistryOpen</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)
[**ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437)
[**ZwEnumerateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566447)
 [ **ZwEnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566453)
[**ZwFlushKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566457) 
 [**ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)
[**ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)
[**ZwQueryValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567069) 
 [ **ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)
 

 





