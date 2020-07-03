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
ms.openlocfilehash: deccc4e3b92f44b1bd7cf29d905d7bf14266e39f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917604"
---
# <a name="kstimedpinsetdevicestate-rule-"></a>KsTimedPinSetDeviceState rule ()


KsTimedPinSetDeviceState 規則は、avstream (KS) ミニポートドライバーが AVStream ミニドライバーの[*Avstrminipinsetdevicestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)ルーチンを使用して、必要な時間内に状態遷移を行うことを指定します。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00082001) |

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
<p>たとえば、次のように入力します。</p>
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>こちらもご覧ください
--------

[*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)
 

 





