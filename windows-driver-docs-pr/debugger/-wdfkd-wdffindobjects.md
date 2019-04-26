---
title: wdfkd.wdffindobjects
description: Wdfkd.wdffindobjects 拡張機能は、WDF オブジェクトのメモリを検索します。
ms.assetid: 8c0a4881-9417-481b-82f8-f3510af768a1
keywords:
- デバッグ wdfkd.wdffindobjects Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdffindobjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c23082fc3c233d19c429ec8bc6df3277aa23094
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341715"
---
# <a name="wdfkdwdffindobjects"></a>!wdfkd.wdffindobjects


**! Wdfkd.wdffindobjects**拡張機能は、WDF オブジェクトのメモリを検索します。

```dbgcmd
!wdfkd.wdffindobjects [StartAddress [Flags]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
(省略可能)。 検索を開始する必要があるアドレスを指定します。 これを省略すると、検索を開始位置から最も最近 **! wdfkd.wdffindobjects**検索が終了しました。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示する情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、「0x0」です。 *フラグ*いなければ使用できません*StartAddress*を指定します。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
詳細な出力が表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
内部の表示では、ハンドルの情報を入力します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

次の例の出力を表示する、 **! wdfkd.wdffindobjects**拡張機能。 0x1 フラグは、2 番目の例で設定されます。

```dbgcmd
1: kd> !wdffindobjects 0xfffffa600211b668 
  Address             Value               Object
  ------------------  ------------------  ------------------
  0xfffffa600211b668  0x0000000000000008  
  0xfffffa600211b670  0xfffffa8002e7b1f0  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b678  0x0000000000000004  
  0xfffffa600211b680  0x0000000000000001  
  0xfffffa600211b688  0xfffffa8006aa3640  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b690  0x0000000000000000  
  0xfffffa600211b698  0xfffff80001e61f78  
  0xfffffa600211b6a0  0x0000000000000010  
  0xfffffa600211b6a8  0x0000000000010286  
  0xfffffa600211b6b0  0xfffffa600211b6c0  
  0xfffffa600211b6b8  0x0000000000000000  
  0xfffffa600211b6c0  0xfffffa8006aa3640  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b6c8  0x0000057ffd184e08  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b6d0  0x0000000000000000  
  0xfffffa600211b6d8  0x0000057ffc51ea18  !WDFMEMORY 0x0000057ffc51ea18
  0xfffffa600211b6e0  0x0000000000000000  

1: kd> !wdffindobjects 0xfffffa600211b668 1 
  Address             Value               Type    Object
  ------------------  ------------------  ------  ------------------
  0xfffffa600211b668  0x0000000000000008  
  0xfffffa600211b670  0xfffffa8002e7b1f0  Object  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b678  0x0000000000000004  
  0xfffffa600211b680  0x0000000000000001  
  0xfffffa600211b688  0xfffffa8006aa3640  Object  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b690  0x0000000000000000  
  0xfffffa600211b698  0xfffff80001e61f78  
  0xfffffa600211b6a0  0x0000000000000010  
  0xfffffa600211b6a8  0x0000000000010286  
  0xfffffa600211b6b0  0xfffffa600211b6c0  
  0xfffffa600211b6b8  0x0000000000000000  
  0xfffffa600211b6c0  0xfffffa8006aa3640  Object  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b6c8  0x0000057ffd184e08  Handle  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b6d0  0x0000000000000000  
  0xfffffa600211b6d8  0x0000057ffc51ea18  Handle  !WDFMEMORY 0x0000057ffc51ea18
  0xfffffa600211b6e0  0x0000000000000000  
```

 

 





