---
title: wdfkd.wdfiotarget
description: Wdfkd.wdfiotarget 拡張機能では、指定した I/O ターゲット オブジェクトに関する情報が表示されます。
ms.assetid: 60a864cc-5099-4d8c-8712-1ba48bce1e0f
keywords:
- デバッグ wdfkd.wdfiotarget Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfiotarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be901cadae35767aa6a6536502858a39528f3bd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571710"
---
# <a name="wdfkdwdfiotarget"></a>!wdfkd.wdfiotarget


**! Wdfkd.wdfiotarget**拡張機能は、指定した I/O ターゲット オブジェクトに関する情報を表示します。

```dbgcmd
!wdfkd.wdfiotarget Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
I/O ターゲット オブジェクトへのハンドル。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 表示する情報の種類を指定するフラグ。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、「0x0」です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示の I/O ターゲットの保留中の要求オブジェクトごとの詳細が含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>コメント
-------

次の例には表示から、 **! wdfkd.wdfiotarget**拡張機能。

```dbgcmd
kd> !wdfiotarget 0x7c9630b8 

# WDFIOTARGET 8369cf40
=========================
WDFDEVICE: 0x7ca7b1c0
Target Device:  !devobj 0x81ede5d8
Target PDO: !devobj 0x822b8a90

Type: Instack target
State:  WdfIoTargetStarted

Requests waiting: 0

Requests sent: 0

Requests sent with ignore-target-state: 0
```

前の例の出力には、I/O ターゲットの親 framework デバイスと共に、オブジェクト、WDM デバイスのアドレスのアドレスが含まれています\_ターゲット ドライバーのデバイス オブジェクトとターゲット デバイスのを表すオブジェクトの構造体。物理デバイス オブジェクト (PDO)。

 

 





