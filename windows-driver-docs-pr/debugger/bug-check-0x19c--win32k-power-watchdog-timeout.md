---
title: バグチェック 0x19C WIN32K_POWER_WATCHDOG_TIMEOUT
description: WIN32K_POWER_WATCHDOG_TIMEOUT バグチェックの値は0x0000019C です。 これは、Win32k が、適切なタイミングでモニターをオンにしなかったことを示します。
ms.assetid: 55907359-C282-43F0-92FE-5DC248BF9D02
keywords:
- バグチェック 0x19C WIN32K_POWER_WATCHDOG_TIMEOUT
- WIN32K_POWER_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_POWER_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae048f4e73c8d518a2471e92e598f377dfac4790
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534653"
---
# <a name="bug-check-0x19c-win32k_power_watchdog_timeout"></a>バグチェック 0x19C: WIN32K \_ 電源 \_ ウォッチドッグ \_ タイムアウト


WIN32K \_ 電源 \_ ウォッチドッグタイムアウトのバグチェックには、 \_ 0x0000019c という値があります。 これは、Win32k が、適切なタイミングでモニターをオンにしなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="win32k_power_watchdog_timeout-parameters"></a>WIN32K \_ 電源 \_ ウォッチドッグの \_ タイムアウトパラメーター


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
<td align="left">「パラメーター1」を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">「パラメーター1」を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">「パラメーター1」を参照してください。</td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。







