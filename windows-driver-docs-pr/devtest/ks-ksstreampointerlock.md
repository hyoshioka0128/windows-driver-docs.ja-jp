---
title: KsStreamPointerLock ロック規則 ()
description: Ksk Streampounlock 規則は、カーネルストリーミング (KS) ミニポートドライバーが Ksk Streampounlock 関数および Ksstreamポインターロック解除関数を正しい順序で使用することを指定します。
ms.assetid: 365C8656-57F1-4774-9859-B67D64403BB3
ms.date: 05/21/2018
keywords:
- KsStreamPointerLock ロック規則 ()
topic_type:
- apiref
api_name:
- KsStreamPointerLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddd7849cacceec25e981da764a06df50d3759f3e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916759"
---
# <a name="ksstreampointerlock-rule-"></a>KsStreamPointerLock ロック規則 ()


Ksk Streampounlock 規則は、カーネルストリーミング (KS) ミニポートドライバーが[**Ksk streampounlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)関数および[**ksstreamポインターロック解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)関数を正しい順序で使用することを指定します。

つまり、ミニポートドライバーは、既にロックされているストリームポインターをロックすることはできません。また、ロックされていないストリームポインターのロックを解除しようとすることもできません。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツールの \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081003) |

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

 

 

 





