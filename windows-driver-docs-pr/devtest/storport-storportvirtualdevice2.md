---
title: StorPortVirtualDevice2 ルール (storport)
description: このルールでは、ことを確認 HwStorFindAdapter ルーチンからの終了時、ポート VirtualDevice フィールドに\_構成\_情報 (Storport) 構造体を TRUE に設定されています。 ルールは、仮想 StorPort ミニポートにのみ適用されます。
ms.assetid: CBD1FAD0-9D85-4989-9CCA-00F5698F5383
ms.date: 05/21/2018
keywords:
- StorPortVirtualDevice2 ルール (storport)
topic_type:
- apiref
api_name:
- StorPortVirtualDevice2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6f75b930b1b52a0433f6e3e0172da8dd497bd736
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528011"
---
# <a name="storportvirtualdevice2-rule-storport"></a>StorPortVirtualDevice2 ルール (storport)


終了時にこの規則を確認、 [ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390) 、ルーチン、 **VirtualDevice**フィールドに、 [**ポート\_構成\_情報 (Storport)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)構造に設定されている**TRUE**します。 ルールは、仮想 StorPort ミニポートにのみ適用されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortVirtualDevice2</strong>ルール。</p>
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

 

 





