---
title: ZwRegistryCreate ルール (storport)
description: このルールは、ZwCreateKey で作成されたレジストリ キーを識別するハンドルはその他の ZwXxx ルーチンで正しく使用される、その後ことを確認します。
ms.assetid: 38CCE6AA-BA42-4305-B193-CB1B1C0F105B
ms.date: 05/21/2018
keywords:
- ZwRegistryCreate ルール (storport)
topic_type:
- apiref
api_name:
- ZwRegistryCreate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4af5884a8b0ee6024dc2de318feb7903d21051e7
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391777"
---
# <a name="zwregistrycreate-rule-storport"></a>ZwRegistryCreate ルール (storport)


このルールは、のレジストリ キーを識別するハンドルが作成されたことを確認します。 [ **ZwCreateKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)他で正しく使用されて、その後*ZwXxx*ルーチン。 [ **ZwOpenKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)ルーチンは、既に開いているハンドルを呼び出さないでください。 ルーチン[ **ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratekey)、 [ **ZwEnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratevaluekey)、 [ **ZwFlushKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwflushkey)、 [ **ZwQueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerykey)、 [ **ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryvaluekey)、 [ **ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwsetvaluekey)、 [ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)、および[ **ZwDeleteKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey)でないと呼ばれる必要があります、開いていないハンドル。 返す前にハンドルを閉じてもする必要があります。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>ZwRegistryCreate</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)
[**ZwDeleteKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey) 
[ **ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratekey)
[**ZwEnumerateValueKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratevaluekey) 
 [ **ZwFlushKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwflushkey)
[**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)
[**ZwQueryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerykey)
 [ **ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryvaluekey)
[**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwsetvaluekey)
 

 





