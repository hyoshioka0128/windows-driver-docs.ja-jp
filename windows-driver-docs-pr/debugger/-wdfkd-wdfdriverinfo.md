---
title: wdfkd.wdfdriverinfo
description: Wdfkd.wdfdriverinfo 拡張機能では、そのデバイス ツリーを含む、指定したドライバーに関する情報とバージョン情報が表示されます。
ms.assetid: dc758fd3-1226-46e3-b249-2cf37ef3e539
keywords:
- デバッグ wdfkd.wdfdriverinfo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdriverinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 675b7f1eea24bd62561f53896033d9f0b3bf5496
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558977"
---
# <a name="wdfkdwdfdriverinfo"></a>!wdfkd.wdfdriverinfo


**! Wdfkd.wdfdriverinfo**拡張機能は、そのデバイス ツリー、ドライバーを使用すると、コンパイルされたカーネル モード ドライバー フレームワーク (KMDF) ライブラリのバージョンの一覧を含む、指定したドライバーに関する情報を表示しますframework デバイス ドライバーを作成するオブジェクト。

```dbgcmd
!wdfkd.wdfdriverinfo [DriverName [Flags]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
(省略可能)。 ドライバーの名前。 *DriverName* .sys ファイル名拡張子を含めることはできません。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示する情報の種類を指定するフラグ。 *フラグ*次のビットの組み合わせにすることができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示では、ドライバーの検証の設定が含まれ、WDF のオブジェクト数も含まれます。 このフラグをビット 6 と組み合わせることができます (0x40) 内部のオブジェクトを表示します。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
ディスプレイは、ドライバーの KMDF ハンドルの階層が含まれます。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
表示は、ハンドルのコンテキストとコールバック関数の情報が含まれます。 このフラグは有効なビット 4 のみ (0x10) を設定します。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>ビット 6 (0x40)  
表示は、各ハンドルに関する追加情報が含まれます。 このフラグは有効なビット 4 のみ (0x10) を設定します。 このフラグは、ビット 0 (0x1) 内部のオブジェクトを表示すると組み合わせることができます。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>ビット 7 (0x80)  
ハンドルの情報がよりコンパクトな形式で表示されます。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>ビット 8 (0x100)  
表示では、内部的な型情報を左揃えされます。 このフラグは有効なビット 4 のみ (0x10) を設定します。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>ビット 9 (0x200)  
ディスプレイは、ドライバーが漏洩した可能性があるハンドルが含まれます。 KMDF version 1.1 以降では、このフラグをサポートします。 このフラグは有効なビット 4 のみ (0x10) を設定します。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>ビット 10 (0x400)  
表示は、詳細な形式で、デバイス ツリーに含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

省略した場合、 *DriverName*パラメーター、既定のドライバーを使用します。 使用して、既定のドライバーを表示することができます、 [ **! wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md) ; 拡張機能を使用して、既定のドライバーを設定することができます、 [ **! wdfkd.wdfsetdriver**](-wdfkd-wdfsetdriver.md)拡張機能。

次の例は、表示から、 **! wdfkd.wdfdriverinfo**拡張機能。

```dbgcmd
## kd> !wdfdriverinfo wdfrawbusenumtest 
----------------------------------
Default driver image name:   wdfrawbusenumtest
WDF library image name:      Wdf01000
 FxDriverGlobals  0x83b7af18
 WdfBindInfo      0xf22250ec
##    Version        v1.5 build(1234)
----------------------------------
WDFDRIVER: 0x7cbc90d0

    !WDFDEVICE 0x7ca7b1c0
            context:  dt 0x83584ff8 ROOT_CONTEXT (size is 0x1 bytes)
             <no associated attribute callbacks>

    !WDFDEVICE 0x7cad31c8
            context:  dt 0x8352cff0 RAW_PDO_CONTEXT (size is 0xc bytes)
             <no associated attribute callbacks>
```

 

 





