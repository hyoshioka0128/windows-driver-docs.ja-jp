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
ms.openlocfilehash: 81a3b065cfc2821e1b01ce61c4733920e279e308
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839422"
---
# <a name="ksstreampointerlock-rule-"></a>KsStreamPointerLock ロック規則 ()


Ksk Streampounlock 規則は、カーネルストリーミング (KS) ミニポートドライバーが[**Ksk streampounlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)関数および[**ksstreamポインターロック解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)関数を正しい順序で使用することを指定します。

つまり、ミニポートドライバーは、既にロックされているストリームポインターをロックすることはできません。また、ロックされていないストリームポインターのロックを解除しようとすることもできません。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出され\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)が発生しました (0x00081003) |

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

 

 

 





