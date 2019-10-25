---
title: KsTimedPinSetDeviceState rule ()
description: KsTimedPinSetDeviceState 規則は、avstream (KS) ミニポートドライバーが AVStream ミニドライバーの AVStrMiniPinSetDeviceState ルーチンを使用して、必要な時間内に状態遷移を行うことを指定します。
ms.assetid: 2BDA0358-A3B1-4A47-AA08-8B086041BC52
ms.date: 05/21/2018
keywords:
- KsTimedPinSetDeviceState rule ()
topic_type:
- apiref
api_name:
- KsTimedPinSetDeviceState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92aae9463476549eee147eb47d087bd46f53431e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839419"
---
# <a name="kstimedpinsetdevicestate-rule-"></a>KsTimedPinSetDeviceState rule ()


KsTimedPinSetDeviceState 規則は、avstream (KS) ミニポートドライバーが AVStream ミニドライバーの[*Avstrminipinsetdevicestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)ルーチンを使用して、必要な時間内に状態遷移を行うことを指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00082001) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 ドライバー検証ツールコマンドを入力し、「 <strong>/domain ks</strong>」と指定します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em>&lt;ドライバー&gt;</em></p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>関連項目
--------

[*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)
 

 





