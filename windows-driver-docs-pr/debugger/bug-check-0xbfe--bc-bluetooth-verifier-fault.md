---
title: バグチェック 0xBFE BC_BLUETOOTH_VERIFIER_FAULT
description: BC_BLUETOOTH_VERIFIER_FAULT バグチェックの値は0x00000BFE です。 これは、ドライバーによって違反が発生したことを示します。
ms.assetid: EC1368CE-46A2-4B69-8405-3118503D35C2
keywords:
- バグチェック 0xBFE BC_BLUETOOTH_VERIFIER_FAULT
- BC_BLUETOOTH_VERIFIER_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BC_BLUETOOTH_VERIFIER_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c4f1cae3054da3da996647354e4d82a9ef7f474
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534795"
---
# <a name="bug-check-0xbfe-bc_bluetooth_verifier_fault"></a>バグチェック 0xBFE: BC \_ BLUETOOTH \_ 検証ツールの \_ エラー


BC \_ BLUETOOTH \_ 検証ツールのバグチェックには、 \_ 0x00000bfe という値があります。 これは、ドライバーによって違反が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bc_bluetooth_verifier_fault-parameters"></a>BC \_ BLUETOOTH \_ 検証ツールの \_ エラーパラメーター


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
<td align="left"><p>Bluetooth 検証ツールのエラーのサブタイプ。</p>
<div class="code">
<code>0x1 : An attempt was made to submit a Bluetooth Request Block that is already in use
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x2 : An attempt was made to free a Bluetooth Request Block that is in use
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x3 : An attempt was made to allocate or initialize an invalid BRB type
                  2 - Brb pointer
                  3 - pdo extension (if available)
                  4 - Reserved
            0x4 : Invalid Bluetooth Request Block pointer was submitted
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x5 : A Bluetooth Request Block with an invalid size was submitted
                  2 - Brb pointer
                  3 - Actual Size
                  4 - Expected Size
            0x6 : The IOCTL_BTH_GET_DEVICE_INFO was called with invalid parameters
                  2 - Reserved
                  3 - Reserved
                  4 - Reserved
            0x7 : BRB_L2CA_UNREGISTER_SERVER was submitted with an invalid server handle
                  2 - Server handle
                  3 - Reserved
                  4 - Reserved
            0x8 : BRB_L2CA_CLOSE_CHANNEL was submitted with an invalid channel handle
                  2 - Brb pointer
                  3 - Channel handle
                  4 - Reserved
            0x9 : BRB_SCO_UNREGISTER_SERVER was submitted with an invalid server handle
                  2 - Server handle
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



<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
パラメーター1は違反の種類を示します。 呼び出し履歴を調べて、動作が不適切なドライバーを特定します。








