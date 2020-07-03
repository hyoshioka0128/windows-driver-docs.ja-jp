---
title: Ksstreamポインター複製ルール ()
description: Ksk Streamポインタの複製ルールは、カーネルストリーム (KS) ミニポートドライバーが Ksk Streamポインタ Clone および Ksstreamポインター Delete 関数を正しく使用することを指定します。
ms.assetid: 5ECF0070-0E36-4A91-B9FA-AA0DB7636B0E
ms.date: 05/21/2018
keywords:
- Ksstreamポインター複製ルール ()
topic_type:
- apiref
api_name:
- KsStreamPointerClone
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6667050a01435b37b21d9751256863d7245239c1
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917400"
---
# <a name="ksstreampointerclone-rule-"></a>Ksstreamポインター複製ルール ()


Ksk Streamポインタの複製ルールは、カーネルストリーム (KS) ミニポートドライバーが[**Ksk Streamポインタ clone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)および[**Ksstreamポインター delete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)関数を正しく使用することを指定します。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツールの \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081002) |

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

 

 

 





