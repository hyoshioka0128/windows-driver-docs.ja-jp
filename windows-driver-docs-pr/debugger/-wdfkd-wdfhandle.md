---
title: wdfkd.wdfhandle
description: Wdfkd.wdfhandle 拡張機能には、ハンドルの種類、オブジェクト コンテキストのポインター、および基になるフレームワーク オブジェクトへのポインターなどの指定のフレームワーク オブジェクト ハンドルに関する情報が表示されます。
ms.assetid: 9365218e-2647-4e54-baba-8774d4ab3ae1
keywords:
- デバッグ wdfkd.wdfhandle Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfhandle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d9070b24233fb5a1ed198bbe300ef6ec6deca24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530475"
---
# <a name="wdfkdwdfhandle"></a>!wdfkd.wdfhandle


**! Wdfkd.wdfhandle**コンテキスト ポインター、および framework オブジェクトのポインターを基になるオブジェクトの拡張機能は、ハンドルの種類などの指定のフレームワーク オブジェクト ハンドルに関する情報を表示します。

```dbgcmd
!wdfkd.wdfhandle Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
Framework のオブジェクトへのハンドル。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示する情報の種類を指定するフラグ。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、「0x0」です。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
表示は、指定したハンドルの子オブジェクトのサブツリーが含まれます。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
表示は、指定したハンドルのコンテキストとコールバック関数の情報が含まれます。 このフラグは有効なビット 4 のみ (0x10) を設定します。

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>ビット 6 (0x40)  
表示は、指定したハンドルの追加情報が含まれます。 このフラグは有効なビット 4 のみ (0x10) を設定します。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>ビット 7 (0x80)  
ハンドルの情報がよりコンパクトな形式で表示されます。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>ビット 8 (0x100)  
表示では、内部的な型情報を左揃えされます。 このフラグは有効なビット 4 のみ (0x10) を設定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

次の例の出力を示しています、 **! wdfhandle**ビット 4 で設定を使用して拡張機能、*フラグ*パラメーター (そのため、出力には、子オブジェクトに関する情報が表示されます)。

```dbgcmd
kd> !wdfhandle 0x7ca7b1c0 10 

handle 0x7ca7b1c0, type is WDFDEVICE

Contexts:
    context:  dt 0x83584ff8 ROOT_CONTEXT (size is 0x1 bytes)
     <no associated attribute callbacks>

Child WDFHANDLEs of 0x7ca7b1c0:
    WDFDEVICE 0x7ca7b1c0
        WDFCMRESLIST 0x7ccfb058
        WDFCMRESLIST 0x7cadb058
        WDFCHILDLIST 0x7c72f0c8
        WDFCHILDLIST 0x7cc090c8
        WDFIOTARGET 0x7c9630b8

!wdfobject 0x83584e38
```

前の例では、入力のハンドルは WDFDEVICE オブジェクトを指します。 この特定のデバイス オブジェクトには、5 つの子オブジェクト--WDFCMRESLIST の 2 つのオブジェクト、2 つの WDFCHILDLIST オブジェクトおよび WDFIOTARGET オブジェクトを 1 つがあります。

 

 





