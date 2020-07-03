---
title: KsTimedDeviceCallbacks rule ()
description: KsTimedDeviceCallbacks ルールは、カーネルストリーミング (KS) ミニポートドライバーが500ミリ秒以内にデバイスコールバック関数から戻ることを指定します。
ms.assetid: 05393761-9018-4DAA-B8B5-EFEBBCDAB955
ms.date: 05/21/2018
keywords:
- KsTimedDeviceCallbacks rule ()
topic_type:
- apiref
api_name:
- KsTimedDeviceCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d92ee833af91c8f3aa8cada77aa053162256db9c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917123"
---
# <a name="kstimeddevicecallbacks-rule-"></a>KsTimedDeviceCallbacks rule ()


KsTimedDeviceCallbacks ルールは、カーネルストリーミング (KS) ミニポートドライバーが500ミリ秒以内にデバイスコールバック関数から戻ることを指定します。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00082002) |

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

[ストリーム ポインターのロックとロック解除](https://docs.microsoft.com/windows-hardware/drivers/stream/locking-and-unlocking-stream-pointers)
 

 





