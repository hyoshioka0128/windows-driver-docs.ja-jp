---
title: dreg
description: Dreg 拡張機能により、レジストリ情報が表示されます。
ms.assetid: a54ed14e-eb9d-48fd-877d-d6d0fe4a8d3f
keywords:
- dreg Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dreg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5596e0bff2fe8cd2db543d635295bb6d84df7b87
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025266"
---
# <a name="dreg"></a>!dreg


**! Dreg**拡張機能では、レジストリ情報が表示されます。

```dbgcmd
!dreg [-d|-w] KeyPath[!Value] 
!dreg
```

## <a name="span-idddk__dreg_dbgspanspan-idddk__dreg_dbgspanparameters"></a><span id="ddk__dreg_dbg"></span><span id="DDK__DREG_DBG"></span>パラメータ


<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
バイナリ値を Dword として表示します。

<span id="_______-w______"></span><span id="_______-W______"></span> **-w**   
バイナリ値が単語として表示されます。

<span id="_______KeyPath______"></span><span id="_______keypath______"></span><span id="_______KEYPATH______"></span>キー*パス*   
レジストリキーのパスを指定します。 次のいずれかの省略形で開始できます。

<span id="hklm"></span><span id="HKLM"></span>**hklm**  
HKEY\_ローカル\_マシン

<span id="hkcu"></span><span id="HKCU"></span>**hkcu**  
HKEY\_現在\_ユーザー

<span id="hkcr"></span><span id="HKCR"></span>**hkcr**  
HKEY\_クラス\_ルート

<span id="hku"></span><span id="HKU"></span>**hku**  
HKEY\_ユーザー

省略形が使用されて\_い\_ない場合は、HKEY LOCAL MACHINE と見なされます。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*値*   
表示するレジストリ値の名前を指定します。 アスタリスク (\*) が使用されている場合は、すべての値が表示されます。 *値*を省略すると、すべてのサブキーが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts .dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ntsdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

レジストリの詳細については、Windows Driver Kit (WDK) のドキュメントおよび*Microsoft windows の内部*(Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

**! Dreg**拡張機能は、ユーザーモードのデバッグ中にレジストリを表示するために使用できます。

リモートデバッグでは、リモートコンピューターのレジストリを参照できるため、この方法が最も役立ちます。 また、ユーザーモードのデバッガーをカーネルデバッガーから制御する場合にも役立ちます。これは、ターゲットコンピューターが固定されている場合に、標準のレジストリエディターを実行できないためです。 (この目的では、 [**sleep**](-sleep--pause-debugger-.md)コマンドも使用できます。 詳細については、「[カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。)

また、情報が読みやすい形式で表示されるため、ローカルでデバッグする場合にも便利です。

**! Dreg**がカーネルモードのデバッグ中に使用された場合、表示される結果は、ターゲットコンピューターではなく、ホストコンピューターのものになります。 対象のコンピューターの未加工のレジストリ情報を表示するには、代わりに[ **! reg**](-reg.md)拡張子を使用します。

例をいくつか紹介します。 次の例では、指定されたレジストリキーのすべてのサブキーが表示されます。

```dbgcmd
!dreg hkcu\Software\Microsoft
```

次の例では、指定されたレジストリキーのすべての値が表示されます。

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!*
```

次の例では、指定されたレジストリキーの開始値が表示されます。

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!Start
```

引数を指定せずに**dreg**を入力すると、デバッガーコマンドウィンドウにこの拡張機能の簡単なヘルプテキストが表示されます。

 

 





