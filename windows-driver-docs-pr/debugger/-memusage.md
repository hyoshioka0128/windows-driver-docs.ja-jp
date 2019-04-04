---
title: memusage
description: Memusage 拡張機能では、物理メモリの使用に関する概要統計が表示されます。
ms.assetid: 32796ada-53ee-465f-b284-db6ee5481878
keywords:
- Windows デバッグ memusage
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- memusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b97b825af8dffed4c1d624228e4240a340be28ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560846"
---
# <a name="memusage"></a>! memusage


**! Memusage**拡張機能には、物理メモリの使用に関する概要統計が表示されます。

構文

```dbgcmd
!memusage [Flags]
```

## <a name="span-idddkmemusagedbgspanspan-idddkmemusagedbgspanparameters"></a><span id="ddk__memusage_dbg"></span><span id="DDK__MEMUSAGE_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
次の値のいずれを指定できます。 既定では 0x0 です。

<span id="0x0"></span><span id="0X0"></span>0x0  
PFN データベース内のページの詳細な説明と共に、一般的な概要情報が表示されます。 このタイプの出力の例については、「解説」を参照してください。

<span id="0x1"></span><span id="0X1"></span>0x1  
PFN データベースで変更済みの非書き込みページに関する概要情報のみを表示します.

<span id="0x2"></span><span id="0X2"></span>0x2  
詳細については PFN データベースで変更済みの非書き込みページのみを表示します。

<span id="0x8"></span><span id="0X8"></span>0x8  
のみメモリの使用に関する全般の概要情報が表示されます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

|       |                  |
|-------|------------------|
| モード | カーネル モードのみ |

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

物理メモリの統計情報は、メモリ マネージャーのページのフレーム数 (PFN) のデータベース テーブルから収集されます。

このコマンドでは、対象のコンピュータが取得するデータ量が大きいため、64 ビット モードで実行されている場合に特にに実行するには長い時間がかかります。 PFN データベース読み込み中、カウンターは、その進行状況を示します。 この読み込みプロセスをスピードアップするために COM ポート速度を増やす、 [ **CTRL + A (トグル ボー レート)** ](ctrl-a--toggle-baud-rate-.md)キー、またはを使用して、 [ **.cache (キャッシュ サイズを設定する)** ](-cache--set-cache-size-.md)(おそらく約 10 MB) にキャッシュ サイズを大きくコマンド。

**! Memusage**コマンドを実行中にも使用できます[ローカル カーネル デバッグ](performing-local-kernel-debugging.md)します。

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !memusage
 loading PFN database
loading (98% complete)

Compiling memory usage data (100% Complete).
             Zeroed:     49 (   196 kb)
               Free:      5 (    20 kb)
            Standby:   5489 ( 21956 kb)
           Modified:    714 (  2856 kb)
    ModifiedNoWrite:      1 (     4 kb)
       Active/Valid:  10119 ( 40476 kb)
         Transition:      6 (    24 kb)
            Unknown:      0 (     0 kb)
              TOTAL:  16383 ( 65532 kb)

  Building kernel map
  Finished building kernel map
Scanning PFN database - (99% complete) 

  Usage Summary (in Kb):


Control Valid Standby Dirty Shared Locked PageTables  name

8251a258    12    108     0     0     0     0  mapped_file( cscui.dll )
827ab1b8     8   1708     0     0     0     0  mapped_file( $Mft )
8263c408   908     48     0     0     0     0  mapped_file( win32k.sys )
8252dda8     0    324     0     0     0     0  mapped_file( ShellIconCache )
8272f638   128    112     0   116     0     0  mapped_file( advapi32.dll )
......
82755958     0      4     0     0     0     0  mapped_file( $Directory )
8250b518     0      4     0     0     0     0    No Name for File
8254d8d8     0      4     0     0     0     0  mapped_file( $Directory )
82537be8     0      4     0     0     0     0  mapped_file( Windows Explorer.lnk )

--------  1348      0     0 ----- -----   904  process ( System )
--------   492      0     0 ----- -----    72  process ( winmine.exe )
--------  3364   1384  1396 ----- -----   188  process ( explorer.exe )
--------   972      0     0 ----- -----    88  process ( services.exe )
--------   496   1456   384 ----- -----   164  process ( winmgmt.exe )
--------  1144      0     0 ----- -----   120  process ( svchost.exe )
--------   944      0     0 ----- -----   156  process ( winlogon.exe )
--------   412      0     0 ----- -----    64  process ( csrss.exe )
......
--------    12      0     0 ----- -----     8  process ( wmiadap.exe )

--------   316      0     0 ----- -----     0  pagefile section (346e)
--------  4096      0     0 ----- -----     0  pagefile section (9ad)

--------   884    280    36 -----     0 -----  driver ( ntoskrnl.exe )
--------    88      8     0 -----     0 -----  driver ( hal.dll )
--------     8      0     0 -----     0 -----  driver ( kdcom.dll )
--------    12      0     0 -----     0 -----  driver ( BOOTVID.dll )
......
--------     8      0     0 -----     0 -----  driver ( ndisuio.sys )
--------    16      0     0 -----     0 -----  driver ( dump_scsiport.sys )
--------    56      0     0 -----     0 -----  driver ( dump_aic78xx.sys )
--------  2756   1060   876 -----     0 -----  driver ( Paged Pool )
--------  1936    128   148 -----     0 -----  driver ( Kernel Stacks )
--------     0      0     0 -----     0 -----  driver ( NonPaged Pool )
```

最初の列には、各マップの構造を記述するコントロールの領域の構造体のアドレスが表示されます。 使用して、 [ **! ca** ](-ca.md)拡張機能コマンドでこれらのコントロールの領域を表示します。

<a name="remarks"></a>注釈
-------

使用することができます、 [ **! vm** ](-vm.md)拡張機能コマンドで仮想メモリ使用量を分析します。 この拡張機能は通常より役に立つ **! memusage**します。 メモリ管理の詳細については、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (この本できない場合がありますのいくつかの言語および国。)

[ **! Pfn** ](-pfn.md) PFN データベース内の特定のページ フレームのエントリを表示する拡張機能のコマンドを使用できます。

 

 





