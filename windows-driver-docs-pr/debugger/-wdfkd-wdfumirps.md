---
title: wdfkd.wdfumirps
description: Wdfkd.wdfumirps 拡張機能では、暗黙的なプロセスで保留中の I/O 要求パケット (Irp UM) のユーザー モードの一覧が表示されます。
ms.assetid: 1BFFDAC0-AA1F-434A-BB05-6864810F9B98
keywords:
- デバッグ wdfkd.wdfumirps Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumirps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0ab52b2fcde71bd6d8a1c8ae4f24e0f1ff861d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537715"
---
# <a name="wdfkdwdfumirps"></a>!wdfkd.wdfumirps


**! Wdfkd.wdfumirps**拡張機能で保留中の I/O 要求パケット (Irp UM) のユーザー モードの一覧が表示されます、[暗黙的なプロセス](controlling-threads-and-processes.md)します。

```dbgcmd
!wdfkd.wdfumirps NumberOfIrps Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______NumberOfIrps______"></span><span id="_______numberofirps______"></span><span id="_______NUMBEROFIRPS______"></span> *NumberOfIrps*   
(省略可能)。 に関する情報を表示するための Irp UM 保留中の数を指定します。 場合*NumberOfIrps*にアスタリスク (\*)、または省略すると、すべての UM Irp が表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0x01 です。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
保留中の Irp の詳細を表示します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

または UMDF ホスト プロセス (wudfhost.exe) に関連付けられているユーザー モードのデバッグ セッションでカーネル モードのデバッグ セッションでは、このコマンドを使用することができます。

このコマンドは、ユーザー モードのコマンドと同じ情報を表示します[ **! wudfext.umirps**](-wudfext-umirps.md)します。

使用することができます[ **! プロセス**](-process.md)すべて UMDF ホスト プロセスとしての一覧を取得することができますを使用[ **.process** ](-process--set-process-context-.md)のいずれかに、暗黙的なプロセスを設定するのにはホスト プロセスの UMDF です。 詳細の例では、次を参照してください。 [ **! wdfkd.wdfumdevstacks**](-wdfkd-wdfumdevstacks.md)します。

出力の例を次に示します **! wdfkd.wdfumirps**します。

```dbgcmd
0: kd> !wdfkd.wdfumirps
Number of pending IRPS: 0x4
####  CWudfIrp     Current Type           UniqueId KernelIrp         Device Stack
----  ----------------  --------------------------------------------------  ----
0000  1ab9e90c40   WdfRequestUndefined        0     0                 1ab9eaa6d0
0001  1ab9ebfa90   WdfRequestInternalIoctl    0     0                 1ab9eaa6d0
0002  1ab9ebfd10   WdfRequestInternalIoctl    0     0                 1ab9eaa6d0
0003  1ab9eae370   Power (WAIT_WAKE)          0     ffffe00000c53010  1ab9eaa6d0
```

 

 





