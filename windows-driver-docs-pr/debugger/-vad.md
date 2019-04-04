---
title: vad
description: Vad 拡張機能には、仮想アドレス記述子 (VAD) の詳細または Vad のツリーが表示されます。
ms.assetid: 96bd5a38-016d-4ce9-b128-cc730577be45
keywords:
- 仮想アドレス記述子 (VAD)
- VAD (仮想アドレス記述子)
- アドレス、仮想アドレス記述子 (VAD)
- Windows デバッグ vad
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vad
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6430ba8483ba98c3d2dbaa0a8f3adfeabcdee20f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530369"
---
# <a name="vad"></a>! vad


**! Vad**拡張機能は、仮想アドレス記述子 (VAD) の詳細または Vad のツリーが表示されます。

-   1 つの仮想アドレス記述子 (VAD) の詳細が表示されます。
-   Vad のツリーの詳細が表示されます。
-   モジュールの特定のユーザー モード Vad に関する情報を表示し、そのモジュールのシンボルを読み込むために使用できる文字列を提供します。

```dbgcmd
!vad VAD-Root [Flag]
!vad Address 1
```

## <a name="span-idddkvaddbgspanspan-idddkvaddbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>パラメーター


<span id="_______VAD-Root______"></span><span id="_______vad-root______"></span><span id="_______VAD-ROOT______"></span> *VAD ルート*   
表示される VAD ツリーのルートのアドレス。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *フラグ*   
フォームの表示になりますを指定します。 表示される値は次のとおりです。

<span id="0"></span>0  
VAD ツリー全体に基づいて*VAD ルート*が表示されます。 (これは、既定値です)。

<span id="1"></span>1  
指定された VAD のみ*VAD ルート*が表示されます。 表示より詳細な分析が含まれます。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ユーザー モードのモジュールの仮想アドレスの範囲内のアドレス。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

仮想アドレス記述子の詳細については、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

使用して任意のプロセス VAD のルートのアドレスが見つかりません、 [ **! プロセス**](-process.md)コマンド。

**! Vad**ページングされたメモリ不足がユーザー モードのモジュールのシンボルを読み込む必要がある場合、コマンドが役に立ちます。 詳細については、[マッピング シンボルときに、PEB がページ アウトが](mapping-symbols-when-the-peb-is-paged-out.md)を参照してください。

次の例に示します、 **! vad**拡張機能。

```dbgcmd
kd> !vad 824bc2f8
VAD     level      start      end    commit
82741bf8 ( 1)      78000    78045         8 Mapped  Exe  EXECUTE_WRITECOPY
824ef368 ( 2)      7f6f0    7f7ef         0 Mapped       EXECUTE_READ
824bc2f8 ( 0)      7ffb0    7ffd3         0 Mapped       READONLY
8273e508 ( 2)      7ffde    7ffde         1 Private      EXECUTE_READWRITE
82643fc8 ( 1)      7ffdf    7ffdf         1 Private      EXECUTE_READWRITE

Total VADs:     5  average level:    2  maximum depth: 2

kd> !vad 824bc2f8 1

VAD @ 824bc2f8
  Start VPN:         7ffb0  End VPN:    7ffd3  Control Area:  827f1208
  First ProtoPte: e1008500  Last PTE e100858c  Commit Charge         0 (0.)
  Secured.Flink          0  Blink           0  Banked/Extend:        0 Offset 0
   ViewShare NoChange READONLY

SecNoChange 
```

 

 





