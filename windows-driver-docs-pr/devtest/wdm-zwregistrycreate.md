---
title: ZwRegistryCreate ルール (wdm)
ms.assetid: 7855d9f0-c8f2-42a3-941b-623038c03840
ms.date: 05/21/2018
description: ''
keywords:
- ZwRegistryCreate ルール (wdm)
topic_type:
- apiref
api_name:
- ZwRegistryCreate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0350c99d398b6fe39483190c3e0c6609524cf1e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549379"
---
# <a name="zwregistrycreate-rule-wdm"></a>ZwRegistryCreate ルール (wdm)


**ZwRegistryCreate**規則の指定後呼び出す[ **ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)へのオープン ハンドルを保持している場合にのみ、ドライバーが次のレジストリ関数を呼び出すことができます、レジストリ キー (いずれかの呼び出し前に、 [ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)または[ **ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437)を閉じるかを識別するハンドルを削除しますレジストリ キーの場合):

-   [**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)

-   [**ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437)

-   [**ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)

-   [**ZwEnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566453)

-   [**ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)

-   [**ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)

-   [**ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)

-   [**ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)

このルールは、ドライバーを呼び出してはならないことを指定しますも[ **ZwCreateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566425)または[ **ZwOpenKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567014)に開いているハンドルを既に保持している場合そのレジストリ キー。

最後に、このルールは、ドライバーのディスパッチ ルーチンから返すまたはルーチンをレジストリ キーへの開いているハンドルを保持しているときにキャンセルする必要がありますいないを指定します。

このルールは、ドライバーが呼び出されていることを確認できません[ **ZwCreateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566425)または[ **ZwOpenKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567014)前にレジストリ キーへのハンドルを取得するには閉じるか、削除します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ZwRegistryCreate</strong>ルール。</p>
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
[**ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)
[**ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069) 
 [ **ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)
 

 





