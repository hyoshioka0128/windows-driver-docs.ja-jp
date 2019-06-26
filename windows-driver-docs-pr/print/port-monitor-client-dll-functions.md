---
title: ポート モニター クライアント DLL 関数
description: ポート モニター クライアント DLL 関数
ms.assetid: 41efab1a-0638-4925-90a2-cf68d2306ca6
keywords:
- ポート モニターを WDK の印刷、関数
- クライアント DLL ポート モニター機能 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 345f5472f0a9a29301edb7eead6ab534069f9c52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368976"
---
# <a name="port-monitor-client-dll-functions"></a>ポート モニター クライアント DLL 関数





次の表には、ポート モニター UI の DLL を定義する必要がある関数が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DllEntryPoint</strong></p></td>
<td><p>DLL エントリ ポイントと通常呼ばれる<strong>DllMain</strong>、これは、Microsoft Windows SDK ドキュメントで説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)"><strong>AddPortUI</strong></a></p></td>
<td><p>ポートを作成し、ダイアログ ボックスを表示して構成情報を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui)"><strong>ConfigurePortUI</strong></a></p></td>
<td><p>以前に追加のポートを構成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-deleteportui" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-deleteportui)"><strong>DeletePortUI</strong></a></p></td>
<td><p>ポートを削除します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitorui" data-raw-source="[&lt;strong&gt;InitializePrintMonitorUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitorui)"><strong>InitializePrintMonitorUI</strong></a></p></td>
<td><p>ポート モニター UI の DLL を初期化します。</p></td>
</tr>
</tbody>
</table>

 

 

 




