---
title: irql の拡張機能コマンド
description: Irql の拡張機能では、デバッガー中断する前に、ターゲット コンピューター上のプロセッサの割り込み要求レベル (IRQL) が表示されます。
ms.assetid: 52dd3b9f-c03c-4b90-a01b-25289de67f5a
keywords:
- IRQL
- 割り込み要求レベル
- Windows デバッグ irql
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- irql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 839226d603c273f23fa76d29c73fea927ea23d57
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336370"
---
# <a name="irql"></a>!irql


**! Irql**拡張機能では、デバッガー中断する前に、ターゲット コンピューター上のプロセッサの割り込み要求レベル (IRQL) が表示されます。

```dbgcmd
!irql [Processor] 
```

## <a name="span-idddkirqldbgspanspan-idddkirqldbgspanparameters"></a><span id="ddk__irql_dbg"></span><span id="DDK__IRQL_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
プロセッサを指定します。 プロセッサ番号を入力します。 このパラメーターを省略した場合、デバッガーには、現在のプロセッサの IRQL が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

**! Irql**拡張機能は Windows Server 2003 および以降のバージョンの Windows で使用できるのみです。

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
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Irql の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

ときに、ターゲット コンピューターは、デバッガー、IRQL の変更が、デバッガー中断が保存される直前に有効であったの IRQL に分割します。 **! Irql**拡張機能には、保存した IRQL が表示されます。

同様に、バグ チェックが発生し、クラッシュ ダンプ ファイルが作成されると、クラッシュ ダンプ ファイルに保存された IRQL は、位置 IRQL ではないのバグ チェックする直前に 1 つ、 [ **KeBugCheckEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551961)ルーチンが実行されます。

どちらの場合も、現在の IRQL がディスパッチに対して発生\_レベル、以外である x86 アーキテクチャ。 したがって、このような 1 つ以上のイベントが発生する場合は、表示の IRQL もなりますディスパッチ\_レベル、デバッグ目的で役に立たなくなります。

[ **! Pcr** ](-pcr.md)拡張機能では、すべてのバージョンの Windows では、現在の IRQL が表示されますが、現在の IRQL は通常、役に立ちません。 直前に、バグを確認またはデバッガーの接続が存在していた IRQL がさらに興味深いとでのみ表示されるこの **! irql**します。

カーネルの破損が発生しました、無効なプロセッサ数を指定する、または、デバッガーは、「PRCB アドレスを取得できません」メッセージを表示します。

デュアル プロセッサ x86 のコンピューターからこの拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !irql 0
Debugger saved IRQL for processor 0x0 -- 28 (CLOCK2_LEVEL)

kd> !irql 1
Debugger saved IRQL for processor 0x1 -- 0 (LOW_LEVEL)
```

デバッガーの詳細モードである場合は、IRQL 自体の説明が含まれます。 Itanium プロセッサから例を次に示します。

```dbgcmd
kd> !irql
Debugger saved IRQL for processor 0x0 -- 12 (PC_LEVEL) [Performance counter level]
```

多くの場合、IRQL の数値の意味は、プロセッサによって異なります。 X64 から例を次に示しますプロセッサ。 IRQL 番号が同じで、前の例のように IRQL 意味が異なることに注意してください。

```dbgcmd
kd> !irql
Debugger saved IRQL for processor 0x0 -- 12 (SYNCH_LEVEL) [Synchronization level]
```

 

 





