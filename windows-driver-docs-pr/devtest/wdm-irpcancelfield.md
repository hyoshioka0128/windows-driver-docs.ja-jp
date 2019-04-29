---
title: IrpCancelField ルール (wdm)
description: IrpCancelField ルールでは、IRP の保留があるキャンセル ルーチンを設定するときに、ドライバーが Irp にキャンセル メンバーの値を確認するを指定します。
ms.assetid: e9221436-21ca-47f0-9dc4-e8b1a7a44854
ms.date: 05/21/2018
keywords:
- IrpCancelField ルール (wdm)
topic_type:
- apiref
api_name:
- IrpCancelField
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55a3b6a4b76fa16fb6f562530175c31caf5c6b23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325376"
---
# <a name="irpcancelfield-rule-wdm"></a>IrpCancelField ルール (wdm)


**IrpCancelField**ルールでは、ドライバーがの値を確認するように指定します、 **Irp -&gt;キャンセル**IRP の保留があるキャンセル ルーチンを設定するときにメンバー。

Static Driver Verifier のドライバーの最後に、このルールを適用する[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンとドライバーのディスパッチ ルーチンの最後にします。

ドライバーが IRP のキャンセルを処理する方法については、次を参照してください。 [**同期 IRP キャンセル**](https://msdn.microsoft.com/library/windows/hardware/ff564531)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrpCancelField</strong>ルール。</p>
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

[**IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)
[**IoCsqInsertIrpEx**](https://msdn.microsoft.com/library/windows/hardware/ff549067)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)
 [ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)も参照してください
--------

[**IRP のキャンセルを同期します。**](https://msdn.microsoft.com/library/windows/hardware/ff564531)
 

 





