---
title: logonsession
description: Logonsession 拡張機能には、指定されたログオンセッションに関する情報が表示されます。
ms.assetid: 95746bc0-ab36-43a7-83ad-9f6fdbb15b39
keywords:
- ログオンセッション
- logonsession Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logonsession
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 706f6931b69b29ffa645bfeafe3cee4347ff1318
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025228"
---
# <a name="logonsession"></a>!logonsession


**! Logonsession**拡張機能には、指定されたログオンセッションに関する情報が表示されます。

無料のビルド構文

```dbgcmd
!logonsession LUID
```

チェックされたビルド構文

```dbgcmd
!logonsession LUID [InfoLevel]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______LUID______"></span><span id="_______luid______"></span>*LUID*   
表示するログオンセッションのローカル一意識別子 (LUID) を指定します。 *LUID*が0の場合、すべてのログオンセッションに関する情報が表示されます。

チェックされたビルドのシステムセッションとすべてのシステムトークンに関する情報を表示するには、「 **! logonsession 3e7 1**」と入力します。

<span id="_______InfoLevel______"></span><span id="_______infolevel______"></span><span id="_______INFOLEVEL______"></span>*InfoLevel*   
(チェックされたビルドのみ)表示するトークン情報の量を指定します。 *InfoLevel*パラメーターには、0 ~ 4 の値を指定できます。0は最も少ない情報を表し、4は最も多くの情報を表します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ログオンセッションの詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンを参照してください。 

<a name="remarks"></a>コメント
-------

無料のビルドでのこの拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !logonsession 0

Dumping all logon sessions.

** Session   0 = 0x0
   LogonId     = {0x0 0x0}
   References  = 0
** Session   1 = 0x8ebb50
 LogonId     = {0xe9f1 0x0}
   References  = 21
** Session   2 = 0x6e31e0
   LogonId     = {0x94d1 0x0}
   References  = 1
** Session   3 = 0x8ecd60
   LogonId     = {0x6b31 0x0}
   References  = 0
** Session   4 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session   5 = 0x0
   LogonId     = {0x0 0x0}
   References  = 0
** Session   6 = 0x8e9720
   LogonId     = {0x3e4 0x0}
   References  = 6
** Session   7 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session   8 = 0xa2e160
   LogonId     = {0x3e5 0x0}
   References  = 3
** Session   9 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session  10 = 0x3ca0
   LogonId     = {0x3e6 0x0}
   References  = 2
** Session  11 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session  12 = 0x1cd0
   LogonId     = {0x3e7 0x0}
   References  = 33
** Session  13 = 0xe0000106
 LogonId     = {0x0 0x0}
 References  = 0
14 sessions in the system.
```

任意のポイントで実行を停止するには、CTRL + BREAK (WinDbg の場合) または CTRL + C (KD の場合) を押します。

 

 





