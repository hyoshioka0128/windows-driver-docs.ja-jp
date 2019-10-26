---
title: バグチェック 0xBFE BC_BLUETOOTH_VERIFIER_FAULT
description: BC_BLUETOOTH_VERIFIER_FAULT のバグチェックの値は0x00000BFE です。 これは、ドライバーによって違反が発生したことを示します。
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
ms.openlocfilehash: ff7466bde88fd16f7d8dad3a62b1ff5bbe948cf7
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916225"
---
# <a name="bug-check-0xbfe-bc_bluetooth_verifier_fault"></a>バグチェック 0xBFE: BC\_BLUETOOTH\_検証ツール\_エラー


BC\_BLUETOOTH\_VERIFIER\_エラーのバグチェックには、0x00000BFE という値があります。 これは、ドライバーによって違反が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bc_bluetooth_verifier_fault-parameters"></a>BC\_BLUETOOTH\_検証ツール\_エラーパラメーター


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
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">「パラメーター1」を参照してください。</td>
</tr>
</tbody>
</table>



<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
パラメーター1は違反の種類を示します。 呼び出し履歴を調べて、動作が不適切なドライバーを特定します。








