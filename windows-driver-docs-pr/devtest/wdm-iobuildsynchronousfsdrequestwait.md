---
title: IoBuildSynchronousFsdRequestWait ルール (wdm)
description: IoBuildSynchronousFsdRequestWait ルールは、kewaitforsingleobject の 1 呼び出す必要がある場合は、その保留または PoCallDriver ステータスを返すことを指定します。\_保留します。
ms.assetid: 99C717B3-1125-4DD9-81A8-1DC4F506B719
ms.date: 05/21/2018
keywords:
- IoBuildSynchronousFsdRequestWait ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildSynchronousFsdRequestWait
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d463a6b37525f9f07d93e2f63084def6738f9dfd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325486"
---
# <a name="iobuildsynchronousfsdrequestwait-rule-wdm"></a>IoBuildSynchronousFsdRequestWait ルール (wdm)


**IoBuildSynchronousFsdRequestWait**ルールを指定する[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)場合に呼び出す必要がありますを[ **保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)ステータスを返します\_保留します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildSynchronousFsdRequestWait</strong>ルール。</p>
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

[**IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137) 
 [ **Kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





