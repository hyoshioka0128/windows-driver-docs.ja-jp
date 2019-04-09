---
title: バグ チェック 0x14F PDC_WATCHDOG_TIMEOUT
description: PDC_WATCHDOG_TIMEOUT のバグ チェックでは、0x0000014F の値を持ちます。 これは、システム コンポーネントが割り当てられた時間の期間内に応答が失敗したことを示します。
ms.assetid: 347D31C2-7027-44BD-A0E8-60C6EC3A2030
keywords:
- バグ チェック 0x14F PDC_WATCHDOG_TIMEOUT
- PDC_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PDC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e32ac1bc7aae87850af0128e90bc025d8163ac12
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239267"
---
# <a name="bug-check-0x14f-pdcwatchdogtimeout"></a>バグ チェック 0x14F:PDC\_ウォッチドッグ\_タイムアウト


PDC\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x0000014F の値を持ちます。 これは、システムが終了するを防ぐ、割り当てられた期間内の応答に失敗しました、システムのコンポーネントがスタンバイに接続されていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="pdcwatchdogtimeout-parameters"></a>PDC\_ウォッチドッグ\_タイムアウト パラメーター


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
<td align="left">1</td>
<td align="left">ハングしたコンポーネントのクライアント ID。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>ハングしたコンポーネントのクライアントの種類。</p>
<p>0x1:通知クライアントが応答に失敗しました。</p>
3 番目のパラメーター:通知クライアント (PDC_NOTIFICATION_CLIENT) へのポインター。
パラメーター 4:Pdc へのポインター。PDC_14F_TRIAGE 構造体。
<p>0x2:回復性クライアントは、応答に失敗しました。</p>
3 番目のパラメーター:回復性のクライアント (PDC_RESILIENCY_CLIENT) へのポインター。
パラメーター 4:Pdc へのポインター。PDC_14F_TRIAGE 構造体。
<p>0x3:アクティベーターをクライアントには、長時間の参照が保持されています。</p>
3 番目のパラメーター:アクティブ化クライアントへのポインター (pdc! _PDC_ACTIVATOR_CLIENT)。
パラメーター 4:Pdc へのポインター。PDC_14F_TRIAGE 構造体。
<p>0x100:Win32k は、適切なタイミングでモニターの要求を完了しませんでした。</p>
3 番目のパラメーター:この要求の最新の POWER_MONITOR_REQUEST_REASON 値。
パラメーター 4:内部に、要求を開始する実行パスを示す値。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">2 番目のパラメーターを参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">2 番目のパラメーターを参照してください。</td>
</tr>
</tbody>
</table>


## <a name="resolution"></a>解決方法

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。
 

 

 




