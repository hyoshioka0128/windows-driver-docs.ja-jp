---
title: バグチェック 0x14F PDC_WATCHDOG_TIMEOUT
description: PDC_WATCHDOG_TIMEOUT バグチェックの値は0x0000014F です。 これは、システムコンポーネントが、割り当てられた期間内に応答できなかったことを示します。
ms.assetid: 347D31C2-7027-44BD-A0E8-60C6EC3A2030
keywords:
- バグチェック 0x14F PDC_WATCHDOG_TIMEOUT
- PDC_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PDC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 322991768b03f360017bcea443a9a82001693f53
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534655"
---
# <a name="bug-check-0x14f-pdc_watchdog_timeout"></a>バグチェック 0x14F: PDC \_ ウォッチドッグの \_ タイムアウト


PDC \_ ウォッチドッグの \_ タイムアウトのバグチェックには、0x0000014F という値があります。 これは、システムコンポーネントが、割り当てられた時間内に応答できなかったため、システムがコネクトスタンバイを終了できないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="pdc_watchdog_timeout-parameters"></a>PDC \_ ウォッチドッグの \_ タイムアウトパラメーター


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
<td align="left">ハング状態のコンポーネントのクライアント ID。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>ハング状態のコンポーネントのクライアントの種類。</p>
<p>0x1: 通知クライアントが応答できませんでした。</p>
パラメーター 3: 通知クライアントへのポインター (PDC_NOTIFICATION_CLIENT)。
パラメーター 4: pdc へのポインターPDC_14F_TRIAGE 構造体。
<p>0x2: 回復性クライアントが応答できませんでした。</p>
パラメーター 3: 回復性クライアント (PDC_RESILIENCY_CLIENT) へのポインター。
パラメーター 4: pdc へのポインターPDC_14F_TRIAGE 構造体。
<p>0x3: アクティベータークライアントは、参照を長時間保持していました。</p>
パラメーター 3: ライセンス認証クライアント (pdc! _PDC_ACTIVATOR_CLIENT) へのポインター。
パラメーター 4: pdc へのポインターPDC_14F_TRIAGE 構造体。
<p>0x100: Win32k は、適切なタイミングでモニターオン要求を完了できませんでした。</p>
パラメーター 3: この要求の最新の POWER_MONITOR_REQUEST_REASON 値。
パラメーター 4: 要求を開始するために使用される内部パスを示す値。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター2を参照</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター2を参照</td>
</tr>
</tbody>
</table>


## <a name="resolution"></a>解像度

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 

 

 




