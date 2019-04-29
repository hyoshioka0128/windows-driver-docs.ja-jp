---
title: Enable application verifier
description: Enable application verifier
ms.assetid: a91e244e-e3b6-4975-8385-1da06cc3ae83
keywords:
- アプリケーション検証ツール (グローバル フラグ) を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aba4d70f1af3baef15733bd92db42ddb3d85d14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325102"
---
# <a name="enable-application-verifier"></a>Enable application verifier


## <span id="ddk_enable_application_verifier_dtools"></span><span id="DDK_ENABLE_APPLICATION_VERIFIER_DTOOLS"></span>


**アプリケーション検証ツールを有効にする**ユーザー モード アプリケーション テストのヒープのページ検証などに使用できるようにシステムの機能をフラグのチェック、ロックし、チェックを処理します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>vrf</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x100</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_APPLICATION_VERIFIER</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

このフラグには、最も基本的な検出機能のみができます。 ユーザー モード アプリケーションを確実にテストするには、Application Verifier (appverif.exe) を使用します。 詳細については、次を参照してください。 [Application Verifier](application-verifier.md)します。

 

 





