---
title: .pop (デバッガー状態の復元)
description: .Pop コマンドは、デバッガーの状態が .push (デバッガーの状態を保存) コマンドを使用して既に保存されている状態に復元します。
ms.assetid: 31f94b2a-3597-40e4-845a-d686274e36c3
keywords:
- デバッガーの状態の復元 (.pop) コマンド
- .pop (デバッガーの状態の復元) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .pop (Restore Debugger State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74d8f2f5878de2a13c3e09e00fcec6e03424b9d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334361"
---
# <a name="pop-restore-debugger-state"></a>.pop (デバッガー状態の復元)


**.Pop**コマンドはデバッガーの状態に復元を使用して保存されている以前の状態、 [ **.push (デバッガーの状態を保存)** ](-push--save-debugger-state-.md)コマンド。

```dbgcmd
.pop
.pop /r
.pop /r /q
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
$T0 t19 ドルの擬似レジスタの保存されている値を復元することを指定します。 場合 **/r**が含まれていない場合、これらの値の影響を受けない、 **.pop**コマンド。

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

このコマンドで使用する場合に最も役に立つ[スクリプト](using-script-files.md)と[デバッガー コマンド プログラム](using-debugger-command-programs.md)と、1 つの固定の状態を操作できるようにします。 コマンドが成功した場合、出力は表示されません。

 

 





