---
title: KsTimedPinCallbacks rule ()
description: KsTimedPinCallbacks ルールは、カーネルストリーミング (KS) ミニポートドライバーが500ミリ秒以内に pin コールバック関数から戻ることを指定します。
ms.assetid: 7B8FF078-118F-465C-BF2F-FECF6EAC3568
ms.date: 05/21/2018
keywords:
- KsTimedPinCallbacks rule ()
topic_type:
- apiref
api_name:
- KsTimedPinCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f4ae4305a876ae23a6d09bcd6ab9364d9f6b6dd7
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968527"
---
# <a name="kstimedpincallbacks-rule-"></a>KsTimedPinCallbacks rule ()


KsTimedPinCallbacks ルールは、カーネルストリーミング (KS) ミニポートドライバーが500ミリ秒以内に pin コールバック関数から戻ることを指定します。

**ドライバーモデル: KS**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00082004)


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

 

 

 





