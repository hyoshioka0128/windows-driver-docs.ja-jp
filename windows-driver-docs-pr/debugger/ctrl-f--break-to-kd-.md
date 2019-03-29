---
title: Ctrl + F (中断して KD を起動)
description: Ctrl キーを押しながら F キーでは、コマンドをキャンセルまたはデバッガーを中断します。
ms.assetid: 45bb7eaf-cb79-4fb4-a01d-373bfb1957c3
keywords:
- CTRL + F (KD 中断) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+F (Break to KD)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d35629ef83e832fa147661431be722ed065d9195
ms.sourcegitcommit: 55dfaaca86e07bef7c41fe601e67cbba1b56ef15
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2019
ms.locfileid: "58505150"
---
# <a name="ctrlf-break-to-kd"></a>Ctrl + F (中断して KD を起動)


Ctrl キーを押しながら F キーでは、コマンドをキャンセルまたはデバッガーを中断します。 (このコントロールのキーは、CDB KD 自体のデバッグに使用するときに特に役立ちます)。

```dbgcmd
CTRL+F  ENTER 
```


## <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>デバッガー</strong></p></td>
<td align="left"><p>KD、CDB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

通常の状況では、CTRL キーを押しながら F キーは、標準的な中断コマンドと同じです ([**CTRL + C** ](ctrl-c--break-.md) KD、CDB でと[デバッグ |中断](debug---break.md)または CTRL + BREAK WinDbg でします)。

ただし、cdb KD をデバッグする場合、これら 2 つのキーが異なる動作が。 CTRL + F がターゲット デバッガー (KD) によって傍受されるときに、ホスト デバッガー (CDB) で CTRL + C がインターセプトされます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**.breakin (カーネル デバッガーにブレーク)**](-breakin--break-to-the-kernel-debugger-.md)

 

 






