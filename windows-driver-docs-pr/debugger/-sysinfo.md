---
title: sysinfo
description: Sysinfo 拡張機能を読み取ってからダンプ ファイルまたはライブ システム指定の SMBIOS、Advanced Configuration and Power Interface (ACPI) CPU 情報が表示されます。
ms.assetid: 1637fcc8-54ff-46a4-94f4-0b2df38507d1
keywords:
- Windows デバッグ sysinfo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sysinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0f9c65d2232e157eb39afdfa1f01d86f4aa2012a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551636"
---
# <a name="sysinfo"></a>! sysinfo


**! Sysinfo**拡張機能を読み取ってからダンプ ファイルまたはライブ システム指定の SMBIOS、Advanced Configuration and Power Interface (ACPI) CPU 情報が表示されます。

```dbgcmd
!sysinfo cpuinfo [-csv [-noheaders]]
!sysinfo cpumicrocode [-csv [-noheaders]]
!sysinfo cpuspeed [-csv [-noheaders]]
!sysinfo gbl [-csv [-noheaders]]
!sysinfo machineid [-csv [-noheaders]]
!sysinfo registers
!sysinfo smbios [-csv [-noheaders]] {-debug | -devices | -memory | -power | -processor | -system | -v} 
!sysinfo -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______cpuinfo______"></span><span id="_______CPUINFO______"></span> **cpuinfo**   
プロセッサ情報を表示します。

<span id="_______cpumicrocode______"></span><span id="_______CPUMICROCODE______"></span> **cpumicrocode**   
(GenuineIntel プロセッサのみ)初期およびキャッシュ済みのマイクロ コード プロセッサ バージョンが表示されます。

<span id="_______cpuspeed______"></span><span id="_______CPUSPEED______"></span> **cpuspeed**   
最大値と現在のプロセッサ速度を表示します。

<span id="_______gbl______"></span><span id="_______GBL______"></span> **gbl**   
ACPI テーブルの BIOS の一覧が表示されます。

<span id="_______machineid______"></span><span id="_______MACHINEID______"></span> **machineid**   
SMBIOS、BIOS、ファームウェア、システム、およびベースボードのマシンの ID 情報を表示します。

<span id="_______registers______"></span><span id="_______REGISTERS______"></span> **registers**   
表示のマシンに固有では、(MSRs) を登録します。

<span id="_______smbios______"></span><span id="_______SMBIOS______"></span> **smbios**   
SMBIOS テーブルが表示されます。

<span id="_______-csv______"></span><span id="_______-CSV______"></span> **-csv**   
コンマ区切りの可変長 (CSV) 形式では、すべてのデータを表示します。

<span id="_______-noheaders______"></span><span id="_______-NOHEADERS______"></span> **-noheaders**   
CSV 形式のヘッダーを抑制します。

<span id="_______-debug______"></span><span id="_______-DEBUG______"></span> **-debug**   
標準の形式と CSV 形式の出力を表示します。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span> **-デバイス**   
SMBIOS テーブルでは、デバイスのエントリを表示します。

<span id="_______-memory______"></span><span id="_______-MEMORY______"></span> **-memory**   
SMBIOS テーブルでは、メモリのエントリを表示します。

<span id="_______-power______"></span><span id="_______-POWER______"></span> **電源**   
SMBIOS テーブルでは、電源エントリを表示します。

<span id="_______-processor______"></span><span id="_______-PROCESSOR______"></span> **-processor**   
SMBIOS テーブルでは、プロセッサのエントリを表示します。

<span id="_______-system______"></span><span id="_______-SYSTEM______"></span> **-system**   
SMBIOS テーブルでは、システムのエントリを表示します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細。 SMBIOS テーブルのエントリの詳細が表示されます。

<span id="_______-_______"></span> **-?**   
この拡張機能のデバッガー コマンド ウィンドウでヘルプを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p><strong>Windows XP ベースのシステム</strong></p>
<p><strong>Windows 2003 ベースのシステム</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows XP Service Pack 2 以降</strong></p>
<p><strong>Windows 2003 では、Service Pack 1 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ダンプ ファイルが、クラッシュするシステム ファイル (.dmp) カーネルまたは完全なダンプ ファイルからミニダンプ ファイルに変換されていない場合にのみ、この拡張機能は便利なまたはライブ システムは、起動が完了し、オンライン (たとえば、ログイン プロンプト) では、します。

任意の組み合わせを使用することができます、 **-デバッグ**、 **-デバイス**、 **-メモリ**、 **-power**、 **-プロセッサ**、**-システム**、および **-v**単一の拡張機能コマンドのパラメーター。

次のパラメーターは、特定のシステムでのみサポートされます。

-   **Gbl**パラメーターは、ターゲット コンピューターに ACPI がサポートしている場合にのみは機能します。

-   **Smbios**パラメーターは、ターゲット コンピューターに SMBIOS がサポートされている場合にのみは機能します。

-   **登録**パラメーターでは、MSRs を収集しないために、Itanium ベースの移行先のコンピューターで機能しません。

マイクロソフトは、これらのレコードから個人を特定できる情報 (PII) を削除しようとします。 すべての PII はダンプ ファイルから削除されます。 ただし、ライブ システムでいくつかの PII がまだ削除できません。 その結果、PII フィールドは情報を実際に含まれる場合でも、0 または空のとして報告されます。

含むコマンドの実行を停止する、 **cpuinfo**、 **gbl**、**登録**、または**smbios** 、いつでもパラメーターが ctrl キーを押しながら BREAK キーを押します(WinDbg) で、または CTRL + C (KD) にします。

 

 





