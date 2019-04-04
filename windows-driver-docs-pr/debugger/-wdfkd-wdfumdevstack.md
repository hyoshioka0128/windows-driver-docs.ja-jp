---
title: wdfkd.wdfumdevstack
description: Wdfkd.wdfumdevstack 拡張機能では、暗黙的なプロセスで UMDF デバイス スタックに関する詳細情報が表示されます。
ms.assetid: AB7F2585-B69B-4854-B8BC-438DDA735149
keywords:
- デバッグ wdfkd.wdfumdevstack Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdevstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96e5b85b11a9f4d85f2cfd5117e375406c9f0f0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530233"
---
# <a name="wdfkdwdfumdevstack"></a>!wdfkd.wdfumdevstack


**! Wdfkd.wdfumdevstack**拡張機能で UMDF デバイス スタックに関する詳細情報が表示されます、[暗黙的なプロセス](controlling-threads-and-processes.md)します。

```dbgcmd
!wdfkd.wdfumdevstack DevstackAddress [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DevstackAddress______"></span><span id="_______devstackaddress______"></span><span id="_______DEVSTACKADDRESS______"></span> *DevstackAddress*   
に関する情報を表示するデバイスのスタックのアドレスを指定します。 使用することができます[ **! wdfkd.wdfumdevstacks** ](-wdfkd-wdfumdevstacks.md)暗黙的なプロセスで UMDF デバイス スタックのアドレスを取得します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0x01 です。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
詳細については、デバイス スタックを表示します。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>ビット 7 (0x80)  
内部のフレームワークについての情報を表示します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

または UMDF ホスト プロセス (wudfhost.exe) に関連付けられているユーザー モードのデバッグ セッションでカーネル モードのデバッグ セッションでは、このコマンドを使用することができます。

このコマンドは、ユーザー モードのコマンドと同じ情報を表示します[ **! wudfext.umdevstack**](-wudfext-umdevstack.md)します。

使用する方法の例を次に示します **! wdfumdevstack**します。 まずを使用して[ **! wdfumdevstacks** ](-wdfkd-wdfumdevstacks.md)暗黙的なプロセスで UMDF デバイス スタックを表示します。

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

上記の出力には、デバイス スタック (0x000000a5a3ab5f70) のアドレスが表示されます。 デバイス スタックに関する詳細情報を取得するには、そのアドレスを渡す **! wdfumdevstack**します。 この例では設定、*フラグ*0x80 フレームワークに関する情報が追加のパラメーター。

```dbgcmd
0: kd> !wdfkd.wdfumdevstack 0x000000a5a3ab5f70 0x80
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
      Internal Values:
        wudfhost!WudfDriverAndFxInfo 0x000000a5a3ac21b8
        IUMDFramework: 0x0000000000000000
        IFxMessageDispatch: 0x000000a5a3aba630
        FxDevice 0x000000a5a3ac4fc0
        Modules:
          Driver: wudfhost!CWudfModuleInfo 0x000000a5a3ac18f0
          Fx:     wudfhost!CWudfModuleInfo 0x000000a5a3aca7a0
          wudfx02000!FxDriver: 0x000000a5a3acaaa0
      DevStack XFerMode: Deferred RW: Buffered CTL: Buffered
```

 

 





