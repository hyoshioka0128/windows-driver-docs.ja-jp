---
title: BCDEdit オプションのリファレンス
description: BCDEdit オプションのリファレンス
ms.assetid: 351f8bc3-a228-48a4-bda8-69ee8521a5d3
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1da864941f44a44e98834848d2dc4e1fde37754d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528020"
---
# <a name="bcdedit-options-reference"></a>BCDEdit オプションのリファレンス


*ブート エントリのパラメーター*、または*ブート パラメーター*、構成オプションを表す省略可能なシステムに固有の設定を示します。 ブート パラメーターは、オペレーティング システムのブート エントリを追加することができます。

このセクションでは、開発、テスト、および x86 ベースおよび x64 ベース プロセッサを搭載したコンピューター上のドライバーのデバッグに関連する Windows のサポートされているバージョンのブート オプションについて説明します。 これらのパラメーターは、Windows オペレーティング システムのブート エントリを追加できます。

> [!NOTE]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。

 

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="bcdedit--bootdebug.md" data-raw-source="[&lt;strong&gt;BCDEdit /bootdebug&lt;/strong&gt;](bcdedit--bootdebug.md)"><strong>BCDEdit/bootdebug</strong></a></p></td>
<td align="left"><p><strong>/Bootdebug</strong>ブート オプションを有効または現在または指定した Windows オペレーティング システムのブート エントリのブートのデバッグを無効にします。</p>
<blockquote>
[!Note]<br />
BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。
</blockquote>
 </td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--dbgsettings.md" data-raw-source="[&lt;strong&gt;BCDEdit /dbgsettings&lt;/strong&gt;](bcdedit--dbgsettings.md)"><strong>BCDEdit/dbgsettings</strong></a></p></td>
<td align="left"><p><strong>/Dbgsettings</strong>オプションを設定またはコンピューターの現在のグローバルなデバッガ設定を表示します。 有効またはカーネル デバッガーを無効にする、使用、 <a href="bcdedit--debug.md" data-raw-source="[&lt;strong&gt;BCDEdit /debug&lt;/strong&gt;](bcdedit--debug.md)"> <strong>BCDEdit/debug</strong> </a>オプション。</p>
<blockquote>
[!Note]<br />
BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。
</blockquote>
 </td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--debug.md" data-raw-source="[&lt;strong&gt;BCDEdit /debug&lt;/strong&gt;](bcdedit--debug.md)"><strong>BCDEdit/debug</strong></a></p></td>
<td align="left"><p><strong>/Debug</strong>ブート オプションを有効または指定されたブート エントリまたは現在のブート エントリに関連付けられている Windows オペレーティング システムのカーネルのデバッグを無効にします。</p>
<blockquote>
[!Note]<br />
BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。
</blockquote>
 </td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--deletevalue.md" data-raw-source="[&lt;strong&gt;BCDEdit /deletevalue&lt;/strong&gt;](bcdedit--deletevalue.md)"><strong>BCDEdit/deletevalue</strong></a></p></td>
<td align="left"><p><strong>BCDEdit/deletevalue</strong>コマンドを削除または Windows のブート構成データ ストア (BCD) からのブート エントリのオプション (とその値) を削除します。 使用して、 <strong>BCDEdit/deletevalue</strong>コマンドを使用して追加されたオプションを削除する<a href="bcdedit--set.md" data-raw-source="[&lt;strong&gt;BCDEdit /set&lt;/strong&gt;](bcdedit--set.md)"> <strong>BCDEdit/set</strong> </a>コマンド。 テスト、Windows 7、Windows 8、Windows 8.1、Windows 10 および Windows の以降のバージョンのドライバーをデバッグする際に、ブート エントリのオプションを削除する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--ems.md" data-raw-source="[&lt;strong&gt;BCDEdit /ems&lt;/strong&gt;](bcdedit--ems.md)"><strong>BCDEdit/ems</strong></a></p></td>
<td align="left"><p><strong>/Ems</strong>オプションを有効または指定したオペレーティング システムのブート エントリの緊急管理サービス (EMS) を無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--emssettings.md" data-raw-source="[&lt;strong&gt;BCDEdit /emssettings&lt;/strong&gt;](bcdedit--emssettings.md)"><strong>BCDEdit/emssettings</strong></a></p></td>
<td align="left"><p><strong>/Emssettings</strong>オプションは、コンピューターのグローバルの緊急管理サービス (EMS) の設定を設定します。 有効または EMS を無効にする、使用、 <strong>/ems</strong>オプション。 <strong>/Emssettings</strong>オプションも有効または任意のブート エントリの EMS を無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--set.md" data-raw-source="[&lt;strong&gt;BCDEdit /set&lt;/strong&gt;](bcdedit--set.md)"><strong>BCDEdit/set</strong></a></p></td>
<td align="left"><p><strong>BCDEdit/set</strong>コマンドは、Windows ブート構成データ ストア (BCD) の Windows 7、Windows Server 2008、Windows 8、Windows 8.1、Windows 10、Windows Server 2012、および Windows Server 2012 R2 のブート エントリ オプション値を設定します。 使用して、 <strong>BCDEdit/set</strong>カーネル デバッガーの設定、メモリのオプション、またはテスト署名されたカーネル モード コードまたは負荷代替ハードウェア アブストラクション レイヤー (HAL) を有効にするオプションなどの特定のブート エントリの要素を構成するコマンドとカーネル ファイル。 ブート エントリのオプションを削除するには、使用、 <a href="bcdedit--deletevalue.md" data-raw-source="[&lt;strong&gt;BCDEdit /deletevalue&lt;/strong&gt;](bcdedit--deletevalue.md)"> <strong>BCDEdit/deletevalue</strong> </a>コマンド。</p></td>
</tr>
</tbody>
</table>

 

### <a name="mapping-bootini-options-to-bcdedit-options-and-elements"></a>BCDEdit のオプションと要素にマッピング Boot.ini オプション

次の表では、BCDEdit のオプションを Windows で使用される BCD 要素 (で Boot.ini)、Windows Vista より前のオペレーティング システムで使用されるブート オプションからマッピングを提供します。 については、BCD ブートの要素を参照してください[BCD 参照](https://go.microsoft.com/fwlink/p/?linkid=56420)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Boot.ini</th>
<th align="left">BCDEdit オプション</th>
<th align="left">BCD の要素の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>/3 GB</p></td>
<td align="left"><p><strong>increaseuserva</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_IncreaseUserVa</p></td>
</tr>
<tr class="even">
<td align="left"><p>/BASEVIDEO</p></td>
<td align="left"><p><strong>vga</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_UseVgaDriver</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/BOOTLOG</p></td>
<td align="left"><p><strong>bootlog</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_BootLogInitialization</p></td>
</tr>
<tr class="even">
<td align="left"><p>/中断します。</p></td>
<td align="left"><p><strong>halbreakpoint</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_DebuggerHalBreakpoint</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/なりません</p></td>
<td align="left"><p><strong>/dbgsettings /start</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/デバッグ、BOOTDEBUG</p></td>
<td align="left"><p><strong>/debug</strong></p>
<p><strong>/bootdebug</strong></p></td>
<td align="left"><p>BcdLibraryBoolean_DebuggerEnabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/デバッグ</p></td>
<td align="left"><p><strong>/debug</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_KernelDebuggerEnabled</p></td>
</tr>
<tr class="even">
<td align="left"><p>/デバッグ、/DEBUGPORT =</p></td>
<td align="left"><p><strong>/dbgsettings</strong></p></td>
<td align="left"><p>BcdLibraryInteger_DebuggerType</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/DEBUGPORT=</p></td>
<td align="left"><p><strong>/dbgsettings</strong></p></td>
<td align="left"><p>BcdLibraryInteger_SerialDebuggerPort</p>
<p>BcdLibraryInteger_SerialDebuggerBaudRate</p>
<p>BcdLibraryInteger_1394DebuggerChannel</p>
<p>BcdLibraryString_UsbDebuggerTargetName</p>
<p>BcdLibraryInteger_DebuggerNetHostIP</p>
<p>BcdLibraryInteger_DebuggerNetPort</p>
<p>BcdLibraryBoolean_DebuggerNetDhcp</p>
<p>BcdLibraryString_DebuggerNetKey</p></td>
</tr>
<tr class="even">
<td align="left"><p>/実行します。</p></td>
<td align="left"><p><strong>nx</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_NxPolicy</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/FASTDETECT</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/HAL =</p></td>
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>BcdOSLoaderString_HalPath</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/KERNEL=</p></td>
<td align="left"><p><strong>カーネル</strong></p></td>
<td align="left"><p>BcdOSLoaderString_KernelPath</p></td>
</tr>
<tr class="even">
<td align="left"><p>/MAXMEM=</p></td>
<td align="left"><p><strong>truncatememory</strong></p></td>
<td align="left"><p>BcdLibraryInteger_TruncatePhysicalMemory</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/NODEBUG</p></td>
<td align="left"><p><strong>/debug</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/NOEXECUTE</p></td>
<td align="left"><p><strong>nx</strong> {</p></td>
<td align="left"><p>BcdOSLoaderInteger_NxPolicy</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/NOGUIBOOT</p></td>
<td align="left"><p><strong>quietboot</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_DisableBootDisplay</p></td>
</tr>
<tr class="even">
<td align="left"><p>/NOLOWMEM</p></td>
<td align="left"><p><strong>nolowmem</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_NoLowMemory</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/NOPAE</p></td>
<td align="left"><p><strong>pae</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_PAEPolicy</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ONECPU</p></td>
<td align="left"><p><strong>onecpu</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_UseBootProcessorOnly</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/PAE</p></td>
<td align="left"><p><strong>pae</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_PAEPolicy</p></td>
</tr>
<tr class="even">
<td align="left"><p>/PCILOCK</p></td>
<td align="left"><p><strong>usefirmwarepcisettings</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_UseFirmwarePciSettings</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/リダイレクト</p></td>
<td align="left"><p><strong>/ems</strong></p>
<p><strong>/emssettings</strong> [ <strong>BIOS</strong> ] |</p>
<p>[ <strong>EMSPORT:</strong>{<em>port</em>} | [<strong>EMSBAUDRATE:</strong> {<em>baudrate</em>}] ]</p></td>
<td align="left"><p>BcdOSLoaderBoolean_EmsEnabled</p></td>
</tr>
<tr class="even">
<td align="left"><p>/SOS</p></td>
<td align="left"><p><strong>sos デバッガー</strong></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 ## <a name="see-also"></a>関連項目
 
 [ブート エントリを追加します。](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-boot-entries)

 

 





