---
title: logonsession
description: Logonsession 拡張機能には、指定されたログオン セッションに関する情報が表示されます。
ms.assetid: 95746bc0-ab36-43a7-83ad-9f6fdbb15b39
keywords:
- ログオン セッション
- Windows デバッグ logonsession
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logonsession
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31b45551a4bf8fb778878793b428dd53e69703e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558975"
---
# <a name="logonsession"></a>! logonsession


**! Logonsession**拡張機能は、指定されたログオン セッションに関する情報を表示します。

無料のビルドの構文

```dbgcmd
!logonsession LUID
```

チェック ビルド構文

```dbgcmd
!logonsession LUID [InfoLevel]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______LUID______"></span><span id="_______luid______"></span> *LUID*   
ログオン セッションを表示するには、ローカル一意識別子 (LUID) を指定します。 場合*LUID*は 0、すべてのログオン セッションに関する情報が表示されます。

チェック ビルドでは、システムのセッションとシステムのすべてのトークンに関する情報を表示するには、入力 **! logonsession 3e7 1**します。

<span id="_______InfoLevel______"></span><span id="_______infolevel______"></span><span id="_______INFOLEVEL______"></span> *InfoLevel*   
(チェック ビルドのみ)トークン情報の量が表示されますを指定します。 *InfoLevel*パラメーターが 0 から 0 は最小限の情報と、最も多くの情報を表す 4、4 の値を取ることができます。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ログオン セッションについては、Microsoft Windows SDK のマニュアルを参照し、 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

無料のビルドでは、この拡張機能からの出力の例を次に示します。

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

任意の時点での実行を停止するには、CTRL + BREAK (WinDbg) で、または (KD) では、CTRL + C キーを押します。

 

 





