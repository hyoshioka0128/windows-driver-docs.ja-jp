---
title: DoubleComplete ルール (ndis)
description: DoubleComplete ルールでは、NDIS ドライバーする必要があります完了しないこと、オブジェクト識別子 (OID) 要求を複数回を指定します。
ms.assetid: b79aaf92-3536-4409-ac8d-420a5999409c
ms.date: 05/21/2018
keywords:
- DoubleComplete ルール (ndis)
topic_type:
- apiref
api_name:
- DoubleComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6ec061373c501beda994f4cac5f996ffeb550ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325823"
---
# <a name="doublecomplete-rule-ndis"></a>DoubleComplete ルール (ndis)


DoubleComplete ルールでは、NDIS ドライバーする必要があります完了しないこと、オブジェクト識別子 (OID) 要求を複数回を指定します。

このルールの検証時に、 **MiniportOidRequest**コールバック関数が返す NDIS\_状態\_成功した場合、 **NdisMOidRequestComplete**の関数を呼び出すことがない必要がありますその要求。 ルールで指定する場合も**MiniportOidRequest**ステータスを返します、ドライバーを呼び出して、保留中はならない、 **NdisMOidRequestComplete**関数を複数回の要求。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>DoubleComplete</strong>ルール。</p>
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

[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 

 





