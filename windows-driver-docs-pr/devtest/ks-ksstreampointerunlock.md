---
title: Ksstreamポインタ Unlock rule ()
description: Ksk Streamポインタ Unlock 規則は、ドライバーがアンロードされる前 (またはデバイスが停止される前) に、カーネルストリーミング (KS) ミニポートドライバーがすべてのストリームポインターをロック解除することを指定します。
ms.assetid: 74742111-85C2-44D2-ACDB-BE1D2D468ED5
ms.date: 05/21/2018
keywords:
- Ksstreamポインタ Unlock rule ()
topic_type:
- apiref
api_name:
- KsStreamPointerUnlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea2d1190af1da6e53947de358f12490049965f17
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917129"
---
# <a name="ksstreampointerunlock-rule-"></a>Ksstreamポインタ Unlock rule ()


Ksk Streamポインタ Unlock 規則は、ドライバーがアンロードされる前 (またはデバイスが停止される前) に、カーネルストリーミング (KS) ミニポートドライバーがすべてのストリームポインターをロック解除することを指定します。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081004) |

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

 

 

 





