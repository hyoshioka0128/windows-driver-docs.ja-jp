---
title: ExclusiveResourceAccess ルール (wdm)
description: ExclusiveResourceAccess ルールは、ドライバーが ExReleaseResourceLite または ExReleaseResourceForThreadLite を呼び出す前に ExAcquireResourceExclusiveLite を呼び出すし、ドライバーが ExReleaseResourceLite を呼び出すことを指定しますを指定します。 または。ExReleaseResourceForThreadLite ExAcquireResourceExclusiveLite への後続の呼び出しの前にします。
ms.assetid: 3de539c0-5af2-4ced-8111-44918f4effc4
ms.date: 05/21/2018
keywords:
- ExclusiveResourceAccess ルール (wdm)
topic_type:
- apiref
api_name:
- ExclusiveResourceAccess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09fcfbe63fb7dc78b280ef5e91a5bf94f14d5a8f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363384"
---
# <a name="exclusiveresourceaccess-rule-wdm"></a>ExclusiveResourceAccess ルール (wdm)


**ExclusiveResourceAccess**ルールでは、ドライバーを呼び出すことを指定します[ **ExAcquireResourceExclusiveLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544351)呼び出す前に[ **ExReleaseResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545597)または[ **ExReleaseResourceForThreadLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545585)し、ドライバーを呼び出すことを指定します**ExReleaseResourceLite。** または**ExReleaseResourceForThreadLite**への後続の呼び出しの前に**ExAcquireResourceExclusiveLite**します。

取得、さまざまなリソースを解放する場合、入れ子になった呼び出しが許可されます。 取得するか、同じリソースを解放する入れ子になった呼び出しでは、この規則に違反します。

このルールでは、ルーチンの終了時に、ドライバーが必要なないリソースへの排他アクセスも許可します。 Static Driver Verifier の最後の監視、 **DriverEntry**、 **AddDevice**、 **StartIo**、 **StartDevice**、 **DpcForIsr**、**キャンセル**、**ディスパッチ**、 **RemoveDevice**、および**アンロード**ルーチン。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">この規則で見つかったバグ チェック</td>
<td align="left"></td>
</tr>
</tbody>
</table>

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ExclusiveResourceAccess</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
[**ExReleaseResourceForThreadLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545585) 
 [ **ExReleaseResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545597)も参照してください
--------

[**使用してスピン ロック中にエラーおよびデッドロックの防止**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





