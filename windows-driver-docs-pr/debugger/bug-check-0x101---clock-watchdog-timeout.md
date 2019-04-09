---
title: バグ チェック 0x101 CLOCK_WATCHDOG_TIMEOUT
description: CLOCK_WATCHDOG_TIMEOUT のバグ チェックでは、0x00000101 セカンダリ プロセッサで予期されるクロック割り込みが割り当てられた時間内で受信していないことを示す値を持ちます。
ms.assetid: 2e35d8c5-00b3-4722-b596-a76f38eb5179
keywords:
- バグ チェック 0x101 CLOCK_WATCHDOG_TIMEOUT
- CLOCK_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CLOCK_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d8b7d91ac45282bb1953a584c5dcc554559f73ec
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239833"
---
# <a name="bug-check-0x101-clockwatchdogtimeout"></a>バグ チェック 0x101:クロック\_ウォッチドッグ\_タイムアウト


クロック\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x00000101 値。 これは、マルチプロセッサ システムで、セカンダリのプロセッサで予期されるクロック割り込みが割り当てられた時間内で受信していないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="clockwatchdogtimeout-parameters"></a>クロック\_ウォッチドッグ\_タイムアウト パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>標準のクロック ティックで、クロック割り込みのタイムアウト間隔</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>応答していないプロセッサのプロセッサ制御ブロック (PRCB) のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

指定されたプロセッサの割り込みを処理していません。 通常、これは、プロセッサが応答していないまたはデッドロックがときに発生します。

 

 




