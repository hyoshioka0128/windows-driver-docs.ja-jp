---
title: バグ チェック 0x19C WIN32K_POWER_WATCHDOG_TIMEOUT
description: WIN32K_POWER_WATCHDOG_TIMEOUT のバグ チェックでは、0x0000019C の値を持ちます。 Win32k しなかったにしないこと、モニター適切なタイミングでこれを示します。
ms.assetid: 55907359-C282-43F0-92FE-5DC248BF9D02
keywords:
- バグ チェック 0x19C WIN32K_POWER_WATCHDOG_TIMEOUT
- WIN32K_POWER_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_POWER_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e503919524a307e7d3105639641212a2b45ae55b
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239525"
---
# <a name="bug-check-0x19c-win32kpowerwatchdogtimeout"></a>バグ チェック 0x19C:WIN32K\_POWER\_ウォッチドッグ\_タイムアウト


WIN32K\_POWER\_ウォッチドッグ\_バグ チェックのタイムアウトが 0x0000019C の値を持ちます。 Win32k しなかったにしないこと、モニター適切なタイミングでこれを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="win32kpowerwatchdogtimeout-parameters"></a>WIN32K\_POWER\_ウォッチドッグ\_タイムアウト パラメーター


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
<td align="left"><p>エラーの種類 (win32kbase!POWER_WATCHDOG_TYPE)</p>
<div class="code">
<code>0x10 : The power request queue is not making progress
              2 - Pointer to the thread processing power requests, if any
              3 - Pointer to the win32k user lock
              4 - Pointer to the power request (win32kbase!PPOWERREQUEST) being
                  processed, if any
          0x20 : Calling PO to set power state
              2 - Pointer to the power request worker thread              
              3 - Reserved
              4 - Reserved
          0x30 : Calling GDI to power on
              2 - Pointer to the power request worker thread
              3 - Reserved
              4 - Reserved
          0x40 : Calling DWM to render
              2 - Pointer to the power request worker thread
              3 - Reserved
              4 - Reserved
          0x50 : Calling monitor driver to power on
              2 - Pointer to the power request worker thread
              3 - Reserved
              4 - Reserved</code>
</div></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
</tbody>
</table>










