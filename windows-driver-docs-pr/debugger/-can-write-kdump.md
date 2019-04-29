---
title: can_write_kdump
description: Can_write_kdump 拡張機能は、指定した型のカーネル ダンプ ファイルを記述するターゲット コンピューターに十分なディスク領域があることを確認します。
ms.assetid: e9fdf8a4-3294-4625-a854-5e42a69374a6
keywords:
- カーネル ダンプ
- Windows デバッグ can_write_kdump
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- can_write_kdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0449a7a28fcf85deb17e08f1932bb55d7ea23f5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336905"
---
# <a name="canwritekdump"></a>! できます\_書き込み\_kdump


**! できます\_書き込み\_kdump**拡張機能は、指定した型のカーネル ダンプ ファイルを記述するターゲット コンピューターに十分なディスク領域があることを確認します。

```dbgsyntax
!can_write_kdump [-dn] [Options]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-dn______"></span><span id="_______-DN______"></span> **-dn**   
ターゲット コンピューター上のファイル システムが NTFS ファイル システムであることを指定します。 このパラメーターを省略した場合、ディスクの空き領域の量を特定できないと、警告が表示されます。 ただし、必要な領域の量も表示されます。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションが有効です。

<span id="-t"></span><span id="-T"></span>**-t**  
ミニダンプに十分な領域があるかどうかに、拡張機能が決定する必要がありますを指定します。

<span id="-s"></span><span id="-S"></span>**-s**  
概要カーネル ダンプに十分な領域があるかどうかに、拡張機能が決定する必要がありますを指定します。 これが既定値です。

<span id="-f"></span><span id="-F"></span>**-f**  
拡張機能の完全なカーネル ダンプに十分な領域があるかどうかかを調べることを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ない場合は*オプション*が指定されている場合、概要のカーネル ダンプに十分な領域があるかどうか、拡張機能が決まります。

次の例では、ファイル システムが指定されていません。

```dbgcmd
kd> !can_write_kdump
Checking kernel summary dump...
WARNING: Can't predict how many pages will be used, assuming worst-case.
Physical memory: 285560 KB
Page file size: 1572864 KB
NO: Page file too small
```

 

 





