---
title: wdfkd.wdfusbdevice
description: Wdfkd.wdfusbdevice 拡張機能では、すべての USB インターフェイスおよび構成されているパイプに指定した KMDF の USB デバイス オブジェクト、取り込めば情報が表示されます。
ms.assetid: 94e0a4ef-36a6-4a37-ac4a-5a2ee2678b9a
keywords:
- デバッグ wdfkd.wdfusbdevice Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfusbdevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d83e17bdee8aa1aacae12a6f453856b192904a5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323304"
---
# <a name="wdfkdwdfusbdevice"></a>!wdfkd.wdfusbdevice


! Wdfkd.wdfusbdevice 拡張機能は、指定されたカーネル モード ドライバー フレームワーク (KMDF) の USB デバイス オブジェクトに関する情報を表示します。 この情報には、すべての USB インターフェイスおよびインターフェイスごとに構成されているパイプが含まれています。

```dbgcmd
!wdfkd.wdfusbdevice Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
WDFUSBDEVICE に型指定された USB デバイスのオブジェクトへのハンドル。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 返される情報の種類を変更する 16 進値。 既定値は、「0x0」です。 フラグは、次のビットの任意の組み合わせを指定できます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示は、I/O ターゲットのプロパティが含まれます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示は、各 USB パイプ オブジェクトの I/O ターゲットのプロパティが含まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

 

 





