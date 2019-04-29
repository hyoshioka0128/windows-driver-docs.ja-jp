---
title: cpuinfo
description: Cpuinfo 拡張機能では、ターゲット コンピューターの CPU に関する詳細情報が表示されます。
ms.assetid: 1e7c348b-0de8-4925-b0a9-300391b6064e
keywords:
- Windows デバッグ cpuinfo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cpuinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08183c39fdce0fd111eec941df723c6d5376bd12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334603"
---
# <a name="cpuinfo"></a>!cpuinfo


**! Cpuinfo**拡張機能には、ターゲット コンピューターの CPU に関する詳細情報が表示されます。

構文

```dbgsyntax
!cpuinfo [Processor] 
```

## <a name="span-idddkcpuinfodbgspanspan-idddkcpuinfodbgspanparameters"></a><span id="ddk__cpuinfo_dbg"></span><span id="DDK__CPUINFO_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
表示するプロセッサを指定します。 これを省略した場合は、すべてのプロセッサが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

マルチプロセッサ コンピューターのデバッグの詳細については、次を参照してください。[マルチプロセッサ構文](multiprocessor-syntax.md)します。

<a name="remarks"></a>コメント
-------

**! Cpuinfo**拡張機能のコマンドを実行するときに使用できます[ローカル カーネル デバッグ](performing-local-kernel-debugging.md)します。

X86 ベースのプロセッサによって生成される例を次に示します。

```dbgcmd
kd> !cpuinfo
CP F/M/S Manufacturer  MHz Update Signature Features 
 0 6,1,9 GenuineIntel  198 000000d200000000 000000ff 
```

Itanium ベースのプロセッサによって生成される例を次に示します。

```dbgcmd
kd> !cpuinfo
CP M/R/F/A Manufacturer     SerialNumber     Features         Speed
 0 2,1,31,0 GenuineIntel     0000000000000000 0000000000000001 1300 Mhz
 1 2,1,31,0 GenuineIntel     0000000000000000 0000000000000001 1300 Mhz
```

**CP**列は、プロセッサ数を示します。 **製造元**列は、プロセッサの製造元を指定します。 **MHz**または**速度**列は、使用できる場合 (mhz)、プロセッサの速度を指定します。

X86 ベースのプロセッサまたは x64 ベース プロセッサを**F**列には、プロセッサのファミリ番号が表示されます、 **M**列には、プロセッサ モデル番号が表示されます、 **S**列には、ステップ実行のサイズが表示されます。

Itanium ベースのプロセッサでは、 **M**列には、プロセッサ モデル番号が表示されます、 **R**列には、プロセッサのリビジョン番号が表示されます、 **F**列が表示されます、プロセッサ ファミリの数と**A**列には、アーキテクチャのリビジョン番号が表示されます。

その他の列も表示されます、マシンの特定のアーキテクチャによって異なります。

その他の列と同様に、各エントリに特定の値を解釈する方法の詳細については、プロセッサのマニュアルを参照してください。

 

 





