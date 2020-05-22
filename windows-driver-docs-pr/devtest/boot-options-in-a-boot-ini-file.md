---
title: Boot.ini ファイルでのブート オプション
description: Boot.ini は、システムパーティションのルートにあるテキストファイルです。通常は c:\Boot.ini. です。 Boot.ini には、BIOS ファームウェアを搭載したコンピューター (従来は x86 および x64 ベースのプロセッサを搭載したコンピューター) のブートオプションが格納されます。
ms.assetid: a2593b6d-03df-49d1-ae77-efec4c2ac8be
keywords:
- Boot.ini ファイル (WDK)
- ブートオプション WDK、boot.ini ファイル
ms.date: 04/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 57e80e1002ee7a464682edac0bfc01f40f410354
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769686"
---
# <a name="boot-options-in-a-bootini-file"></a>Boot.ini ファイルでのブート オプション

> [!IMPORTANT] 
> このトピックでは、Windows XP と Windows Server 2003 でサポートされているブートオプションについて説明します。 Windows 8、Windows Server 2012、Windows 7、Windows Server 2008、または Windows Vista のブートオプションを変更する場合は、「 [Windows Vista 以降のブートオプション](boot-options-in-windows-vista-and-later.md)」を参照してください。\]

Boot.ini は、システムパーティションのルートにあるテキストファイル (通常は \\ c: boot.ini) です。 Boot.ini には、従来、IA-32 ベースおよび x64 ベースのプロセッサを搭載したコンピューターの BIOS ファームウェアを搭載したコンピューターのブートオプションが格納されます。 Windows Server 2003 以前のバージョンの Windows NT オペレーティングシステムでは、コンピューターの起動時に、"ntldr" という Windows ブートローダーによって、boot.ini ファイルが読み取られ、ブートメニューに各オペレーティングシステムのエントリが表示されます。 次に、ntldr は Boot.ini ファイルの設定に従って、選択したオペレーティングシステムを読み込みます。

既定では、NTFS ドライブでは、**システム**、**隠し**、**アーカイブ**、および**読み取り**専用の属性が boot.ini を保護するように設定されています。ただし、Administrators グループのメンバーは、これらの属性を変更できます。 ファイル属性は、ブートローダーの動作には影響しません。

以下のセクションでは、Boot.ini について簡単に説明します。また、パーソナルコンピューターの Advanced テクノロジ (PC/AT) が搭載されているコンピューターに固有のブートオプションの側面について説明します。

ここでは、以下の内容について説明します。

- [Boot.ini ファイルの概要](overview-of-the-boot-ini-file.md)
- [Boot.ini ファイルの編集](editing-the-boot-ini-file.md)
- [Boot.ini ファイルのバックアップ](backing-up-the-boot-ini-file.md)

このドキュメントでは、ドライバーの開発者とテスト担当者にとって特に重要な Boot.ini の側面について説明します。 Boot.ini パラメーターの完全な一覧については、Microsoft サポート web サイトの「 [WINDOWS XP と Windows Server 2003 の Boot.ini ファイルの使用可能なスイッチオプション](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)」を参照してください。


## <a name="mapping-bootini-options-to-bcdedit-options-and-elements"></a>ブート .ini オプションを BCDEdit オプションと要素にマッピングしています

次の表は、windows Vista (Boot.ini) より前のオペレーティングシステムで使用されているブートオプションから、Windows で使用される BCDEdit オプションおよび BCD 要素へのマッピングを示しています。 BCD ブート要素と WMI のコンテキストの詳細については、「 [BCD Wmi Provider Reference](https://docs.microsoft.com/previous-versions/windows/desktop/bcd/bcd-reference)」を参照してください。

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
<th align="left">BCD 要素の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>かつ</p></td>
<td align="left"><p><strong>increaseuserva</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_IncreaseUserVa</p></td>
</tr>
<tr class="even">
<td align="left"><p>/BASEVIDEO</p></td>
<td align="left"><p><strong>ボード</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_UseVgaDriver</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/BOOTLOG</p></td>
<td align="left"><p><strong>bootlog</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_BootLogInitialization</p></td>
</tr>
<tr class="even">
<td align="left"><p>中断</p></td>
<td align="left"><p><strong>halbreakpoint</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_DebuggerHalBreakpoint</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/CRASHDEBUG</p></td>
<td align="left"><p><strong>/dbgsettings/start</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/DEBUG、BOOTDEBUG</p></td>
<td align="left"><p><strong>/debug</strong></p>
<p><strong>/bootdebug</strong></p></td>
<td align="left"><p>BcdLibraryBoolean_DebuggerEnabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/DEBUG</p></td>
<td align="left"><p><strong>/debug</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_KernelDebuggerEnabled</p></td>
</tr>
<tr class="even">
<td align="left"><p>/DEBUG、/DEBUGPORT =</p></td>
<td align="left"><p><strong>/dbgsettings</strong></p></td>
<td align="left"><p>BcdLibraryInteger_DebuggerType</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/DEBUGPORT =</p></td>
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
<td align="left"><p>/EXECUTE</p></td>
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
<td align="left"><p><strong>hal.dll</strong></p></td>
<td align="left"><p>BcdOSLoaderString_HalPath</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/KERNEL =</p></td>
<td align="left"><p><strong>カーネル</strong></p></td>
<td align="left"><p>BcdOSLoaderString_KernelPath</p></td>
</tr>
<tr class="even">
<td align="left"><p>/MAXMEM =</p></td>
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
<p>[ <strong>Emsport:</strong>{<em>port</em>} |[<strong>Emsbaudrate レート:</strong> {<em>ボーレート</em>}]]</p></td>
<td align="left"><p>BcdOSLoaderBoolean_EmsEnabled</p></td>
</tr>
<tr class="even">
<td align="left"><p>/SOS</p></td>
<td align="left"><p><strong>sos</strong></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>


