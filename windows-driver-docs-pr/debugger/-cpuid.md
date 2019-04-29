---
title: cpuid
description: Cpuid 拡張機能は、システム上のプロセッサに関する情報を表示します。
ms.assetid: 3dbd1079-d129-4e17-8d06-18b25fdd17c9
keywords:
- Windows デバッグ cpuid
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cpuid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e8d14bc7dd929e900aa632359d526087ea96bbc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334605"
---
# <a name="cpuid"></a>!cpuid


**! Cpuid**拡張機能は、システム上のプロセッサに関する情報を表示します。

```dbgsyntax
!cpuid [Processor]
```

## <a name="span-idddkcpuiddbgspanspan-idddkcpuiddbgspanparameters"></a><span id="ddk__cpuid_dbg"></span><span id="DDK__CPUID_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
その情報が表示されます、プロセッサを指定します。 このパラメーターを省略した場合は、すべてのプロセッサが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

マルチプロセッサ コンピューターをデバッグする方法の詳細については、次を参照してください。[マルチプロセッサ構文](multiprocessor-syntax.md)します。

<a name="remarks"></a>コメント
-------

**! Cpuid**ライブ ユーザー モードまたはカーネル モードのデバッグ、ローカル カーネル デバッグ、およびデバッグ ダンプ ファイルの中の拡張機能の動作します。 ただし、ユーザー モードのミニダンプ ファイルには、アクティブなプロセッサについての情報のみが含まれます。

ユーザー モードでデバッグしている場合、 **! cpuid**拡張機能で、対象のアプリケーションが実行されているコンピューターをについて説明します。 カーネル モードでは、対象のコンピュータがについて説明します。

次の例では、この拡張機能を示します。

```dbgcmd
kd> !cpuid 
CP  F/M/S  Manufacturer        MHz 
 0  6,5,1  GenuineIntel        700 
 1  8,1,5  AuthenticAMD        700 
```

**CP**列は、プロセッサ数を示します。 (これらの数値は常に順次、ゼロから始まります) です。 **製造元**列は、プロセッサの製造元を指定します。 **MHz**列がある場合にプロセッサの速度を指定します。

X86 ベースのプロセッサまたは x64 ベース プロセッサを**F**列には、プロセッサのファミリ番号が表示されます、 **M**列には、プロセッサ モデル番号が表示されます、 **S**列には、ステップ実行のサイズが表示されます。

Itanium ベースのプロセッサでは、 **M**列にはプロセッサ モデル番号が表示され、R 列には、プロセッサのリビジョン番号が表示されます、 **F**列は、プロセッサ ファミリの数、および、が表示されます。**A**列には、アーキテクチャのリビジョン番号が表示されます。

 

 





