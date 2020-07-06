---
title: memusage
description: '[Memusage 拡張機能] には、物理メモリの使用量に関する概要統計が表示されます。'
ms.assetid: 32796ada-53ee-465f-b284-db6ee5481878
keywords:
- memusage ウィンドウのデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- memusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 43000e448c5f7a400eeaccfa73a8a6b832276a4f
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968303"
---
# <a name="memusage"></a>!memusage


**! Memusage**拡張機能には、物理メモリの使用に関する概要統計が表示されます。

Syntax

```dbgcmd
!memusage [Flags]
```

## <a name="span-idddk__memusage_dbgspanspan-idddk__memusage_dbgspanparameters"></a><span id="ddk__memusage_dbg"></span><span id="DDK__MEMUSAGE_DBG"></span>パラメータ


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
次のいずれかの値を指定できます。 既定値は0x0 です。

<span id="0x0"></span><span id="0X0"></span>0x0  
一般的な概要情報と、PFN データベース内のページの詳細な説明が表示されます。 この種類の出力の例については、「解説」を参照してください。

<span id="0x1"></span><span id="0X1"></span>0x1  
PFN データベースの変更された書き込みなしのページに関する概要情報のみを表示します。

<span id="0x2"></span><span id="0X2"></span>0x2  
PFN データベースの変更された書き込みなしページに関する詳細情報のみを表示します。

<span id="0x8"></span><span id="0X8"></span>0x8  
メモリの使用に関する全般的な概要情報のみを表示します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

**モード**: カーネルモードのみ


 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

物理メモリの統計情報は、Memory Manager のページフレーム番号 (PFN) データベーステーブルから収集されます。

このコマンドの実行には長い時間がかかります。特に、対象のコンピュータが64ビットモードで実行されている場合は、取得するデータ量が多いためです。 PFN データベースの読み込み中に、カウンターにその進行状況が表示されます。 この読み込みを高速化するには、 [**CTRL + A (ボーレートの切り替え)**](ctrl-a--toggle-baud-rate-.md)キーを使用して COM ポートの速度を上げるか、 [**. Cache (キャッシュサイズの設定)**](-cache--set-cache-size-.md)コマンドを使用してキャッシュサイズを増やします (おそらく約 10 MB)。

[ローカルカーネルデバッグ](performing-local-kernel-debugging.md)の実行中に、 **! memusage**コマンドを使用することもできます。

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

最初の列には、マップされた各構造体を記述するコントロール領域の構造体のアドレスが表示されます。 これらのコントロール領域を表示するには、 [**! ca**](-ca.md)拡張コマンドを使用します。

<a name="remarks"></a>注釈
-------

[**! Vm**](-vm.md) extension コマンドを使用して、仮想メモリの使用量を分析できます。 この拡張機能は、通常、 **! memusage**よりも便利です。 メモリ管理の詳細については、「 *Microsoft Windows の内部*」 (Mark Russinovich と David ソロモン) を参照してください。 

[**! Pfn**](-pfn.md) extension コマンドを使用すると、pfn データベース内の特定のページフレームエントリを表示できます。

 

 





