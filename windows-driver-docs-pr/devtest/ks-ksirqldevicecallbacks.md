---
title: KsIrqlDeviceCallbacks ルール ()
description: KsIrqlDeviceCallbacks ルールでは、カーネルストリーミング (KS) ミニポートドライバーが、呼び出されたときと同じ IRQL を持つ KS デバイスコールバック関数から返されることを指定します。
ms.assetid: 8C73EE2F-AA5B-478B-925A-C7DC4F6EFF6A
ms.date: 05/21/2018
keywords:
- KsIrqlDeviceCallbacks ルール ()
topic_type:
- apiref
api_name:
- KsIrqlDeviceCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52eaf159b26935dc79edc5f895aca06fb4d9e182
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917922"
---
# <a name="ksirqldevicecallbacks-rule-"></a>KsIrqlDeviceCallbacks ルール ()


KsIrqlDeviceCallbacks ルールでは、カーネルストリーミング (KS) ミニポートドライバーが、呼び出されたときと同じ IRQL を持つ KS デバイスコールバック関数から返されることを指定します。

**デバッグに関するヒント**

ドライバーの検証でこの規則の違反が検出されると、[**バグチェック 0xC4: ドライバー \_ 検証ツールが \_ 検出さ \_ **](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)れた違反を、 *arg1*値が0x00081006 としてトリガーされます。 バグチェックの*arg3* (rulestate) と*arg4* (下位状態) は、規則違反に関する追加情報へのポインターを提供します。

[**! Ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)デバッガー拡張機能を使用して、関数の開始時と終了時の IRQL 値を確認します。

次のコマンドを使用します。

**! ruleinfo 0x81006** *ruleinfo 下位ステータス* *。*

ルールの状態データでは、 *Oldirql*は、コールバックが入力されたときの IRQL です。 *NewIrql*は、コールバック関数が終了したときの IRQL です。

ドライバー検証ツールがバグチェックの前に IRQL を発生させる可能性があるため、 [**! irql**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-irql)を使用して現在の irql を判断しないでください。 代わりに、 **! verifier 0x008**を使用して、IRQL ログを表示します。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081006) |

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

 

 

 





