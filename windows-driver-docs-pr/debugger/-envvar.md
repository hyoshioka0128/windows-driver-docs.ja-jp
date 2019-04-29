---
title: envvar
description: Envvar 拡張機能では、指定された環境変数の値が表示されます。
ms.assetid: 7a6e1796-08e0-414e-a092-326b30c8ce8f
keywords:
- Windows デバッグ envvar
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- envvar
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8da5dffa05b644b6fdeccfa81a4e9fa6ab5f7fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334514"
---
# <a name="envvar"></a>!envvar


**! Envvar**拡張機能は、指定された環境変数の値を表示します。

```dbgcmd
!envvar Variable
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Variable______"></span><span id="_______variable______"></span><span id="_______VARIABLE______"></span> *変数*   
値を表示する環境変数を指定します。 *変数*大文字小文字は区別されません。

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
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

環境変数の詳細については、次を参照してください。[環境変数](environment-variables.md)および Microsoft Windows SDK のドキュメント。

<a name="remarks"></a>注釈
-------

**! Envvar**拡張機能は、ユーザー モードとカーネル モードの両方は機能します。 ただし、カーネル モードでアイドル状態のスレッドを現在のプロセスとして設定するとプロセスの環境ブロック (PEB) へのポインターは**NULL**が失敗したため、します。 カーネル モードで、 **! envvar**拡張機能として次の例は、対象のコンピューターで環境変数が表示されます。

```dbgcmd
0:000> !envvar _nt_symbol_path
        _nt_symbol_path = srv*C:\mysyms*https://msdl.microsoft.com/download/symbols
```

 

 





