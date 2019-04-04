---
title: wdfkd.wdfumirp
description: Wdfkd.wdfumirp 拡張機能では、ユーザー モードの I/O 要求パケット (IRP UM) に関する情報が表示されます。
ms.assetid: 8706E8F6-A387-48A9-AF14-ED2C0F94AD98
keywords:
- デバッグ wdfkd.wdfumirp Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39c9546381135db9ecd25c765062e5177896d71d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535941"
---
# <a name="wdfkdwdfumirp"></a>!wdfkd.wdfumirp


**! Wdfkd.wdfumirp**拡張機能は、ユーザー モードの I/O 要求パケット (IRP UM) に関する情報を表示します。

```dbgcmd
!wdfkd.wdfumirp Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
に関する情報を表示するには、UM IRP のアドレスを指定します。 使用することができます[ **! wdfkd.wdfumirps** ](-wdfkd-wdfumirps.md)で UM Irp のアドレスを取得、[暗黙的なプロセス](controlling-threads-and-processes.md)します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

または UMDF ホスト プロセス (wudfhost.exe) に関連付けられているユーザー モードのデバッグ セッションでカーネル モードのデバッグ セッションでは、このコマンドを使用することができます。

このコマンドは、ユーザー モードのコマンドと同じ情報を表示します[ **! wudfext.umirp**](-wudfext-umirp.md)します。

使用することができます[ **! プロセス**](-process.md)すべて UMDF ホスト プロセスとしての一覧を取得することができますを使用[ **.process** ](-process--set-process-context-.md)のいずれかに、暗黙的なプロセスを設定するのにはホスト プロセスの UMDF です。 詳細の例では、[ **! wdfkd.wdfumdevstacks**](-wdfkd-wdfumdevstacks.md)を参照してください。

使用する方法を次に示します[ **! wdfkd.wdfumirps** ](-wdfkd-wdfumirps.md)と **! wdfkd.wdfumirp**個々 の UM IRP に関する情報を表示します。

```dbgcmd
0: kd> !wdfkd.wdfumirps
Number of pending IRPS: 0x4
####  CWudfIrp     Current Type           UniqueId KernelIrp         Device Stack
----  ----------------  --------------------------------------------------  ----
...
0003  1ab9eae370   Power (WAIT_WAKE)          0     ffffe00000c53010  1ab9eaa6d0

0: kd> !wdfkd.wdfumirp 1ab9eae370
UM IRP: 0x0000001ab9eae370  UniqueId: 0x0  Kernel Irp: 0xffffe00000c53010
  Type: Power (WAIT_WAKE)
  ClientProcessId: 0x0
  Device Stack: 0x0000001ab9eaa6d0
  IoStatus
    hrStatus: 0x0
    Information: 0x0
  Total number of stack locations: 2
  CurrentStackLocation: StackLocation[ 0 ]
  > StackLocation[ 0 ]
      FxDevice:   (None)
      Completion:
        Callback:   0x0000000000000000
        Context:    0x0000001ab9ebc750
    StackLocation[ 1 ]
    ...
```

 

 





