---
title: wdfkd.wdfumdevstacks
description: Wdfkd.wdfumdevstacks 拡張機能では、暗黙的なプロセスですべて UMDF デバイス スタックに関する情報が表示されます。
ms.assetid: 05D09B0D-4ED8-4333-B4BC-5BE28C63312C
keywords:
- デバッグ wdfkd.wdfumdevstacks Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdevstacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc189f5294c8de6a1ce9d10ecff28ffdfe2ad1e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572458"
---
# <a name="wdfkdwdfumdevstacks"></a>!wdfkd.wdfumdevstacks


**! Wdfkd.wdfumdevstacks**拡張機能のすべての UMDF デバイス スタックに関する情報を表示する、[暗黙的なプロセス](controlling-threads-and-processes.md)します。

```dbgcmd
!wdfkd.wdfumdevstacks [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0x01 です。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
詳細については各デバイス スタックを表示します。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>ビット 7 (0x80)  
内部のフレームワークについての情報を表示します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>コメント
-------

または UMDF ホスト プロセス (wudfhost.exe) に関連付けられているユーザー モードのデバッグ セッションでカーネル モードのデバッグ セッションでは、このコマンドを使用することができます。

このコマンドは、ユーザー モードのコマンドと同じ情報を表示します[ **! wudfext.umdevstacks**](-wudfext-umdevstacks.md)します。

このコマンドを使用する前に使用して[ **! プロセス**](-process.md) UMDF のすべてのホスト プロセスの一覧を取得します。

```dbgcmd
0: kd> !process 0 0 wudfhost.exe
PROCESS ffffe00000c32900
    SessionId: 0  Cid: 079c    Peb: 7ff782537000  ParentCid: 037c
    DirBase: 607af000  ObjectTable: ffffc00009807940  HandleCount: <Data Not Accessible>
    Image: WUDFHost.exe
```

上記の出力は、1 つ UMDF ホスト プロセスがあることを示しています。つまり、wudfhost.exe の 1 つのインスタンスがあります。

次を使用して[ **.process** ](-process--set-process-context-.md) wudfhost.exe に暗黙的なプロセスを設定します。

```dbgcmd
0: kd> .process /P ffffe00000c32900
Implicit process is now ffffe000`00c32900
.cache forcedecodeptes done
```

使用して **! wdfkd.wdfumdevstacks**暗黙的なプロセス (wudfhost.exe) で UMDF デバイス スタックを表示します。

```dbgcmd
0: kd> !wdfkd.wdfumdevstacks
Number of device stacks: 1
  Device Stack: 0x000000a5a3ab5f70     Pdo Name: \Device\00000052
    Active: Yes
    Number of UM devices: 1
    Device 0
      Driver Config Registry Path: MyUmdf2Driver
      UMDriver Image Path: C:\WINDOWS\System32\drivers\UMDF\MyUmdf2Driver.dll
      FxDriver: 0xa5a3acaaa0
      FxDevice: 0xa5a3ac4fc0
      Open UM files (use !wdfumfile <addr> for details): <None>
      Device XFerMode: Deferred RW: Buffered CTL: Buffered
      DevStack XFerMode: Deferred RW: Buffered CTL: Buffered
```

上記の出力は、暗黙的なプロセスに 1 つの UMDF デバイス スタックがあることを示しています。 デバイス スタックが 1 つのデバイス オブジェクトを表示することも (UM 数のデバイス。1).

 

 





