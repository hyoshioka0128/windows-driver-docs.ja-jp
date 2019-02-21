---
title: IoBuildSynchronousFsdRequestWaitTimeout ルール (wdm)
description: このドライバーは下まで無期限に待機されていることを検出した場合、IoBuildSynchronousFsdRequestWaitTimeout ルール レポート欠陥 IRP のイベントがシグナル状態になる完了ルーチンで必要なドライバーが返されます。
ms.assetid: 8344C597-BD71-4953-95F0-F912C31EF52A
ms.date: 05/21/2018
keywords:
- IoBuildSynchronousFsdRequestWaitTimeout ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildSynchronousFsdRequestWaitTimeout
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53ed10d9976abb84836b5508b08037ef23ad803d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536234"
---
# <a name="iobuildsynchronousfsdrequestwaittimeout-rule-wdm"></a>IoBuildSynchronousFsdRequestWaitTimeout ルール (wdm)


**IoBuildSynchronousFsdRequestWaitTimeout**ルールは、このドライバーは下まで無期限に待機されていることを検出した場合、問題を報告 IRP のイベントがシグナル状態になる完了ルーチンで必要なドライバーが返されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildSynchronousFsdRequestWaitTimeout</strong>ルール。</p>
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
 

 





