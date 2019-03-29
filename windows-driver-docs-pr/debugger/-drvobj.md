---
title: drvobj
description: Drvobj 拡張機能では、DRIVER_OBJECT に関する詳細情報が表示されます。
ms.assetid: 98f3cacf-311c-4000-8336-4964cc2cb9b0
keywords:
- Windows デバッグ drvobj
ms.date: 11/16/2018
topic_type:
- apiref
api_name:
- drvobj
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfebfb5d30d2005303cc2f6def4a297e733574e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579922"
---
# <a name="drvobj"></a>!drvobj


**! Drvobj**拡張機能は、ドライバーに関する詳細情報を表示します。\_オブジェクト。

```dbgcmd
!drvobj DriverObject [Flags] 
```

## <a name="span-idddkdrvobjdbgspanspan-idddkdrvobjdbgspanparameters"></a><span id="ddk__drvobj_dbg"></span><span id="DDK__DRVOBJ_DBG"></span>パラメーター


<span id="_______DriverObject______"></span><span id="_______driverobject______"></span><span id="_______DRIVEROBJECT______"></span> *DriverObject*   
ドライバーのオブジェクトを指定します。 ドライバーの 16 進数のアドレス指定できます\_オブジェクトの構造体またはドライバーの名前。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
次のビットの組み合わせにすることができます。 (既定では 0x01。)

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ドライバーが所有するデバイス オブジェクトが表示をによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
ドライバーのディスパッチ ルーチンのエントリ ポイントを含めるようにディスプレイをによりします。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
(ビット 0 (0x1) が必要)、ドライバーが所有するデバイス オブジェクトの詳細な情報を一覧します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)例と、この拡張機能コマンドのアプリケーション。 ドライバーのオブジェクトについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

## <a name="remarks"></a>コメント
-------

場合*DriverObject*デバイスの名前を指定しますが、プレフィックス、プレフィックスを提供しない"\\ドライバー\\"と見なされます。 このコマンドでかどうかをチェックする注*DriverObject*式エバリュエーターを使用する前に有効なアドレスまたはデバイス名は、します。

場合*DriverObject* 、アドレスは、ドライバーのアドレスがあります\_オブジェクトの構造体。 これは、ドライバーに渡される引数を調べることで取得できます**DriverEntry**ルーチン。

この拡張機能のコマンドは、指定したドライバーによって作成されたすべてのデバイス オブジェクトの一覧に表示されます。 このドライバー オブジェクトに登録されているすべての高速な I/O ルーチンも表示されます。

機能を持ってロジック 810 SCSI ミニポート ドライバーの例を次に示します。

```dbgcmd
kd> bp DriverEntry          //  breakpoint at DriverEntry

kd> g
symc810!DriverEntry+0x40:    
80006a20: b07e0050 stl     t2,50(sp)

kd> r a0  //address of DevObj (the first parameter)
a0=809d5550

kd> !drvobj 809d5550   //  display the driver object
Driver object is for:
\Driver\symc810
Device Object list:
809d50d0
```

使用することも[ **! devobj 809d50d0** ](-devobj.md)デバイス オブジェクトに関する情報を取得します。

 

 





