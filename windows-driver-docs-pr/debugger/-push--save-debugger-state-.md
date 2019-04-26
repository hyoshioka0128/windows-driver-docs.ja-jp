---
title: .push (デバッガー状態の保存)
description: .Push コマンドは、デバッガーの現在の状態を保存します。
ms.assetid: 2e0b45d6-35b8-4c86-9c54-df8d16b4dcc2
keywords:
- .push (デバッガーの状態を保存) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .push (Save Debugger State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12e52dd705ed1c0581bad4e3308bd3db336ecdd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335741"
---
# <a name="push-save-debugger-state"></a>.push (デバッガー状態の保存)


**.Push**コマンドは、デバッガーの現在の状態を保存します。

```dbgcmd
.push
.push /r
.push /r /q
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
現在の擬似レジスタに値が指定 **$t0**に**ドル t19**保存する必要があります。 場合、 **/r**パラメーターが使用されないこれらの値はでは保存されません場合、 **.push**コマンド。

<span id="________q______"></span><span id="________Q______"></span> **/q**   
コマンドがサイレント モードで実行されることを指定します。 つまり、任意の出力を表示せず、コマンドを実行します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>



<a name="remarks"></a>注釈
-------

このコマンドで使用する場合に最も役に立つ[スクリプト](using-script-files.md)と[デバッガー コマンド プログラム](using-debugger-command-programs.md)と、1 つの固定の状態を操作できるようにします。 デバッガーを以前にこのコマンドを使用して保存された状態に復元するには、使用、 [ **.pop (デバッガーの状態の復元)** ](-pop--restore-debugger-state-.md)コマンド。 コマンドが成功した場合、出力は表示されません。









