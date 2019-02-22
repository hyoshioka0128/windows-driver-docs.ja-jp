---
title: システムの構文
description: システムの構文
ms.assetid: f2b327cd-8ba5-45f3-9116-756df82358f4
keywords:
- システムでは、コマンドの構文
- (システム識別子)
- システム、システム識別子)
- システムのコマンドの構文規則
- (システム識別子)、コマンドの構文規則
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4acefb5c143f880f05225fcc6b58591f32f624d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531379"
---
# <a name="system-syntax"></a>システムの構文


## <span id="ddk_system_syntax_dbg"></span><span id="DDK_SYSTEM_SYNTAX_DBG"></span>


多くのデバッガー コマンドでは、そのパラメーターとしてプロセスの識別子を持ちます。

システム識別子の前に、2 つの縦棒 (|) が表示されます。 システム識別子には、次の値のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">システム識別子</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>||.</strong></p></td>
<td align="left"><p>現在のシステム</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>||#</strong></p></td>
<td align="left"><p>現在の例外のデバッグ イベントの原因となったシステム。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>||*</strong></p></td>
<td align="left"><p>すべてのシステムです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>||</strong><em>ddd</em></p></td>
<td align="left"><p>序数はシステム<em>ddd</em>します。</p></td>
</tr>
</tbody>
</table>



システムには、デバッガーは、それらへの順序で序数が割り当てられます。

デバッグの開始時に現在のシステムが例外またはデバッグ イベント (または、1 つ、デバッガーが最後に接続されている) の原因となったものにします。 使用して、新しいものを指定するまで、システムが現在のシステムが変更される、 [ **| |s (現在のシステムの設定)** ](--s--set-current-system-.md)コマンドまたはを使用して、[プロセスとスレッド ウィンドウ](processes-and-threads-window.md)WinDbg でします。

<a name="example"></a>例
-------
この例では、次の 3 つのダンプ ファイルが読み込まれるを示します。 システム 1 はアクティブで、システム 2 は、デバッグ イベントを発生します。

```dbgcmd
||1:1:017> ||
   0 User mini dump: c:\notepad.dmp
.  1 User mini dump: c:\paint.dmp
#  2 User mini dump: c:\calc.dmp
```


<a name="remarks"></a>注釈
-------

複数のシステムを操作するに使用することができます、 [.opendump](-opendump--open-dump-file-.md)と同時に複数のクラッシュ ダンプをデバッグします。 複数のターゲットのセッションを制御する方法の詳細については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

**注**コマンドのデバッグの種類ごとに異なる方法で動作しているために、ライブのターゲットと、ダンプ ターゲットをデバッグするときに、問題があります。 たとえば、使用する場合、 **g (移動)** コマンドの場合は、現在のシステムは、ダンプ ファイル、デバッガーが実行を開始がすることはできません戻るデバッガーに割り込む、break コマンドが認識されないため、ダンプ ファイルのデバッグの有効とします。








