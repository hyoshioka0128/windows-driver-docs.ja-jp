---
title: wudfext.umdevstacks
description: Wudfext.umdevstacks 拡張機能では、現在のホスト プロセスですべてのデバイス スタックに関する情報が表示されます。
ms.assetid: e69420fc-97b8-420f-b635-bee41fbf4586
keywords:
- デバッグ wudfext.umdevstacks Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umdevstacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36d9a0b21a0966a740ceff55acac81017a4afa44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572419"
---
# <a name="wudfextumdevstacks"></a>!wudfext.umdevstacks


**! Wudfext.umdevstacks**拡張機能は、現在のホスト プロセスですべてのデバイス スタックに関する情報を表示します。

```dbgcmd
!wudfext.umdevstacks [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0x01 です。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
詳細については各デバイス スタックを表示します。

<span id="Bit_8__0x80_"></span><span id="bit_8__0x80_"></span><span id="BIT_8__0X80_"></span>8 ビット (0x80)  
内部のフレームワークについての情報を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wudfext.dll

 
### <a name="remarks"></a>コメント
-------

**! Wudfext.umdevstacks**拡張機能は、各デバイス スタックに関連付けられている framework インターフェイス オブジェクトを表示します。 出力の使用の詳細については **! wudfext.umdevstacks**を参照してください[ **! wudfext.umdevstack**](-wudfext-umdevstack.md)します。

**! Wudfext.umdevstacks**出力に「オブジェクトを追跡」と「Refcount 追跡」という 2 つのフィールドが含まれています。 これらを示すかどうか追跡オプション オブジェクト (**TrackObjects**) と、参照カウントを追跡オプション (**TrackRefCounts**) 有効になっている WDF Verifier でそれぞれ。 オブジェクト トラッカー アドレス; が含まれるオブジェクトの追跡オプションが有効になっている場合このアドレスに渡すことが[ **! wudfext.wudfdumpobjects** ](-wudfext-wudfdumpobjects.md)追跡情報を表示します。

次の例に示します、 **! wudfext.umdevstacks**表示。

```dbgcmd
0: kd> !umdevstacks 
Number of device stacks: 1
  Device Stack: 0x038c6f08    Pdo Name: \Device\USBPDO-11
    Number of UM devices: 1
    Device 0
      Driver Config Registry Path: WUDFOsrUsbFx2
      UMDriver Image Path: D:\Windows\system32\DRIVERS\UMDF\WUDFOsrUsbFx2.dll
      Fx Driver: IWDFDriver 0x3076ff0
      Fx Device: IWDFDevice 0x3082e70
        IDriverEntry: WUDFOsrUsbFx2!CMyDriver 0x0306eff8
      Open UM files (use !umfile <addr> for details): 
        0x04a8ef84
      Device XFerMode: CopyImmediately RW: Buffered CTL: Buffered
      Object Tracker Address: 0x03074fd8
        Object   Tracking ON
        Refcount Tracking OFF
    DevStack XFerMode: CopyImmediately RW: Buffered CTL: Buffered
```


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[ユーザー モード ドライバー フレームワークのデバッグ](user-mode-driver-framework-debugging.md)を参照してください。
 

 





