---
title: wdfkd.wdfcrashdump
description: Wdfkd.wdfcrashdump 拡張機能では、データが存在する場合のエラー ログの情報と、ミニダンプ ファイルからその他のクラッシュ ダンプの情報を表示します。
ms.assetid: 419c76b1-e291-4503-8c59-aa46140e40b3
keywords:
- デバッグ wdfkd.wdfcrashdump Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfcrashdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5de525a7ffeee84d06f2a0073f86030d6d67f1fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550983"
---
# <a name="wdfkdwdfcrashdump"></a>!wdfkd.wdfcrashdump


**! Wdfkd.wdfcrashdump**データが存在する場合のエラー ログの情報と、ミニダンプ ファイルからその他のクラッシュ ダンプの情報を拡張機能が表示されます。

KMDF

```dbgcmd
!wdfkd.wdfcrashdump [InfoType]
```

UMDF

```dbgcmd
!wdfkd.wdfcrashdump [DriverName.dll][-d | -f | -m]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______InfoType______"></span><span id="_______infotype______"></span><span id="_______INFOTYPE______"></span> *InfoType*   
表示する情報の種類を指定します。 *情報の種類*は省略可能であり、次の値のいずれかを指定できます。

<span id="log"></span><span id="LOG"></span>**log**  
クラッシュ ダンプ ファイルで使用可能な場合は、エラー ログの情報を表示します。 これが既定値です。

<span id="loader"></span><span id="LOADER"></span>**ローダー**  
ミニダンプの動的バインドのドライバーが表示されます。

<span id="drivername.dll"></span><span id="DRIVERNAME.DLL"></span>*DriverName*.dll  
UMDF ドライバーの名前を指定します。 .Dll ファイルのサフィックスを含める必要があります。 この省略可能なパラメーターを省略すると、メタデータ、読み込まれたモジュール一覧、および使用可能なログ出力が含まれます。

<span id="-d"></span><span id="-D"></span>**-d**  
ドライバーのログのみが表示されます。

<span id="-f"></span><span id="-F"></span>**-f**  
フレームワークのログのみが表示されます。

<span id="-m"></span><span id="-M"></span>**-m**  
フレームワークとドライバーのログ記録された順序でをマージします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF

UMDF 2.15

<a name="remarks"></a>注釈
-------

この例は、使用する方法を示します **! wdfkd.wdfcrashdump** KMDF ドライバーに関する情報を表示します。 指定した場合**ローダー**の*情報の種類*出力には、動的バインド ドライバーにはミニダンプ ファイルが含まれています。

```dbgcmd
0: kd> !wdfcrashdump loader 
Retrieving crashdump loader information...
## Local buffer 0x002B4D00, bufferSize 720
----------------------------------------------
  ImageName      Version    FxGlobals

  Wdf01000       v1.9(6902)
  msisadrv       v1.9(6913) 0x84deb260
  vdrvroot       v1.9(6913) 0x860e8260
  storflt        v1.5(6000) 0x861dfe90
  cdrom          v1.9(6913) 0x84dca008
  intelppm       v1.9(6913) 0x864704a8
  HDAudBus       v1.7(6001) 0x86101c98
  1394ohci       v1.7(6001) 0x8610d2e8
  CompositeBus   v1.9(6913) 0x86505b98
  ObjTestClassExt v1.9(6902) 0x865b7f00
  mqfilter       v1.9(6902) 0x865b8008
  mqueue         v1.9(6902) 0x865b6910
  umbus          v1.9(6913) 0x8618aea0
  monitor        v1.9(6913) 0x86aac1d8
  PEAUTH         v1.5(6000) 0x854e5350
----------------------------------------------
```

この例は、使用する方法を示します **! wdfkd.wdfcrashdump** UMDF ドライバーに関する情報を表示します。 発行した場合 **! wdfkd.wdfcrashdump**パラメーターなしの出力には、失敗したホスト プロセスで、クラッシュおよび読み込まれたすべてのドライバーの一覧の原因となったドライバーが含まれます。 この一覧にログが関連付けられているドライバーをクリックすることができます。

```dbgcmd
0:001> !wdfkd.wdfcrashdump
Opening minidump at location C:\temp\WudfHost_ext__1312.dmp

Faulting driver: wpptest.dll
Failure type: Unhandled Exception (WUDFUnhandledException)
Faulting thread ID: 2840

Listing all drivers loaded in this host process at the time of the failure:

  ServiceName
  wpptest 
  CoverageCx0102
  coverage
  WUDFVhidmini
  ToastMon
  WUDFOsrUsbFilter
```

上記の例では、出力には、WER レポートのイベントの種類であるエラーの種類が含まれます。 ここでは、できる**WUDFVerifierFailure**または**WUDFUnhandledException**します。 詳細については、[WER レポートでの UMDF メタデータにアクセスする](https://msdn.microsoft.com/library/windows/hardware/ff542975)を参照してください。 UMDF の出力には、イベントの種類がある場合、エラー コードが含まれます**WUDFVerifierFailure**します。

フレームワークのエラー ログの記録を表示する、[完全メモリ ダンプ](complete-memory-dump.md)、[カーネル メモリ ダンプ](kernel-memory-dump.md)、または[ライブのカーネル モード ターゲット](live-kernel-mode-targets.md)、試すこともできます、 [**! wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md)拡張機能。

**追加情報**

実行中のトレース レコーダーには、ドライバーを有効にする方法については、[を使用して転送トレース レコーダー (IFR) KMDF および UMDF 2 ドライバー](https://msdn.microsoft.com/library/windows/hardware/dn940485)を参照してください。 ドライバーを WDF のデバッグの詳細については、[デバッグ WDF ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540790)を参照してください。 KMDF のデバッグ方法の詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!wdfkd.wdflogdump**](-wdfkd-wdflogdump.md)

[**!wdfkd.wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md)

 

 






