---
title: KsIrqlFilterCallbacks バック規則 ()
description: KsIrqlFilterCallbacks 規則は、カーネルストリーミング (KS) ミニポートドライバーが、コールバック関数が呼び出されたときと同じ IRQL を持つ KS フィルターコールバック関数から戻ることを指定します。
ms.assetid: AC27FF93-DC7C-4287-B3D6-2579FAA65A77
ms.date: 05/21/2018
keywords:
- KsIrqlFilterCallbacks バック規則 ()
topic_type:
- apiref
api_name:
- KsIrqlFilterCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d55161a628053dd89321787548b0b058854b714e
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968163"
---
# <a name="ksirqlfiltercallbacks-rule-"></a>KsIrqlFilterCallbacks バック規則 ()


KsIrqlFilterCallbacks 規則は、カーネルストリーミング (KS) ミニポートドライバーが、コールバック関数が呼び出されたときと同じ IRQL を持つ KS フィルターコールバック関数から戻ることを指定します。

**デバッグに関するヒント**

ドライバーの検証でこの規則の違反が検出されると、[**バグチェック 0xC4: ドライバー \_ 検証ツールが \_ 検出さ \_ **](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)れた違反を、 *arg1*値が0x00081007 としてトリガーされます。 バグチェックの*arg3* (rulestate) と*arg4* (下位状態) は、規則違反に関する追加情報へのポインターを提供します。

[**! Ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)デバッガー拡張機能を使用して、関数の開始時と終了時の IRQL 値を確認します。

次のコマンドを使用します。

**! ruleinfo 0x81007** *ruleinfo* *下位の。*

ルールの状態データでは、 *Oldirql*は、コールバックが入力されたときの IRQL です。 *NewIrql*は、コールバック関数が終了したときの IRQL です。

ドライバー検証ツールがバグチェックの前に IRQL を発生させる可能性があるため、 [**! irql**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-irql)を使用して現在の irql を判断しないでください。 代わりに、 **! verifier 0x008**を使用して、IRQL ログを表示します。

**ドライバーモデル: KS**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081007)


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
<p>次に例を示します。</p>
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





