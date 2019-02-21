---
title: ZwRegistryOpen ルール (wdm)
ms.assetid: c98682c3-0d38-4d5b-9649-7574106f9ce3
ms.date: 05/21/2018
description: ''
keywords:
- ZwRegistryOpen ルール (wdm)
topic_type:
- apiref
api_name:
- ZwRegistryOpen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a61e568b5d3335a9f53741535f633026d59e065e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530392"
---
# <a name="zwregistryopen-rule-wdm"></a>ZwRegistryOpen ルール (wdm)


[ **ZwRegistryOpen** ](storport-zwregistryopen.md)規則の指定後呼び出す[ **ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)ドライバーは、次のレジストリ関数のみを呼び出す開いているハンドルをレジストリ キーを押しながら (つまり、呼び出す前に[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)または[ **ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437))。

-   [**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)

-   [**ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437)

-   [**ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)

-   [**ZwEnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566453)

-   [**ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)

-   [**ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)

-   [**ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)

-   [**ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)

このルールは、ドライバーを呼び出してはならないことを指定しますも[ **ZwOpenKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567014)レジストリ キーへの開いているハンドルが保持既に場合。

最後に、このルールは、ドライバーのディスパッチ ルーチンから返すまたはルーチンをレジストリ キーへの開いているハンドルを保持しているときにキャンセルする必要がありますいないを指定します。

このルールは、ドライバーが保持しているハンドルが開いているを適切なレジストリ キーを呼び出すときに検証されません[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)または[ **ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437).

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)
[**ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)
[**ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437) 
[ **ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)
[**ZwEnumerateValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566453) 
 [ **ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)
[**ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)
[**ZwQueryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567060)
 [ **ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)
[**ZwSetValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567109)も参照してください
--------

[**ZwRegistryCreate**](wdm-zwregistrycreate.md)
 

 





