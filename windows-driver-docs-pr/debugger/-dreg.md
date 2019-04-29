---
title: dreg
description: Dreg 拡張機能には、レジストリ情報が表示されます。
ms.assetid: a54ed14e-eb9d-48fd-877d-d6d0fe4a8d3f
keywords:
- Windows デバッグ dreg
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dreg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 163f816b7026bafb6091f5cae9c42d77a9c2769c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334555"
---
# <a name="dreg"></a>!dreg


**! Dreg**拡張機能には、レジストリ情報が表示されます。

```dbgcmd
!dreg [-d|-w] KeyPath[!Value] 
!dreg
```

## <a name="span-idddkdregdbgspanspan-idddkdregdbgspanparameters"></a><span id="ddk__dreg_dbg"></span><span id="DDK__DREG_DBG"></span>パラメーター


<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
Dword として表示されるエラーの原因のバイナリ値。

<span id="_______-w______"></span><span id="_______-W______"></span> **-w**   
単語として表示されるエラーの原因のバイナリ値。

<span id="_______KeyPath______"></span><span id="_______keypath______"></span><span id="_______KEYPATH______"></span> *KeyPath*   
レジストリ キーのパスを指定します。 次の省略形のいずれかでそれを開始できます。

<span id="hklm"></span><span id="HKLM"></span>**hklm**  
HKEY\_ローカル\_マシン

<span id="hkcu"></span><span id="HKCU"></span>**hkcu**  
HKEY\_現在\_ユーザー

<span id="hkcr"></span><span id="HKCR"></span>**hkcr**  
HKEY\_クラス\_ルート

<span id="hku"></span><span id="HKU"></span>**hku**  
HKEY\_ユーザー

省略形を使用しない場合 HKEY\_ローカル\_マシンが前提としています。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *値*   
表示されるレジストリ値の名前を指定します。 場合、アスタリスク (\*) が使用すると、すべての値が表示されます。 場合*値*は省略すると、すべてのサブキーが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

レジストリの詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

**! Dreg**拡張機能は、ユーザー モードのデバッグ中にレジストリを表示するために使用できます。

リモート コンピューターのレジストリを参照することができ、リモート デバッグ時に便利です。 これも便利です、カーネル デバッガーからユーザー モードのデバッガーを管理するときに固定されているときに、ターゲット コンピューターの標準レジストリ エディターを実行することはできませんので。 (使用することができます、 [ **.sleep** ](-sleep--pause-debugger-.md)もこの目的のコマンド。 参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします)。

情報と、ローカルでデバッグが読みやすい形式で表示されるにも便利です。

場合 **! dreg**されるカーネル モードのデバッグ中に表示される結果は、ホスト コンピューターとターゲット コンピューターではなくになります。 ターゲット コンピューターの生のレジストリ情報を表示するには、使用、 [ **! reg** ](-reg.md)拡張子代わりにします。

例をいくつか紹介します。 指定されたレジストリ キーのすべてのサブキーは、次の場合に表示するされます。

```dbgcmd
!dreg hkcu\Software\Microsoft
```

次が表示されますすべての値で指定されたレジストリ キー。

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!*
```

次の値が表示されます、開始、指定したレジストリ キー。

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!Start
```

入力 **! dreg**せず、任意の引数は、デバッガー コマンド ウィンドウでこの拡張機能の簡単なヘルプ テキストを表示します。

 

 





