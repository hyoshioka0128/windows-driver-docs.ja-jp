---
title: WdbgExts 関数
description: WdbgExts 関数
ms.assetid: 1b070b0c-575d-4104-af66-e0a2c2f2c1b6
keywords:
- WdbgExts 拡張機能、関数
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3308bcc0cbb5a3b01511b67b3b8282741037207f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325846"
---
# <a name="wdbgexts-functions"></a>WdbgExts 関数


## <span id="ddk_wdbgexts_functions_dbwx"></span><span id="DDK_WDBGEXTS_FUNCTIONS_DBWX"></span>


Wdbgexts.h ヘッダー ファイルには、次の関数のプロトタイプが含まれています。 これらの関数は、32 ビットと 64 ビットの両方の拡張機能のプロトタイプを使用します。

[**GetContext**](https://msdn.microsoft.com/library/windows/hardware/ff545736)

[**SetContext**](https://msdn.microsoft.com/library/windows/hardware/ff556644)

[**CheckControlC**](https://msdn.microsoft.com/library/windows/hardware/ff539072)

[**GetCurrentProcessAddr**](https://msdn.microsoft.com/library/windows/hardware/ff545779)

[**GetCurrentProcessHandle**](https://msdn.microsoft.com/library/windows/hardware/ff545816)

[**GetCurrentThreadAddr**](https://msdn.microsoft.com/library/windows/hardware/ff545889)

[**GetDebuggerCacheSize**](https://msdn.microsoft.com/library/windows/hardware/ff546568)

[**GetDebuggerData**](https://msdn.microsoft.com/library/windows/hardware/ff546573)

[**disasm**](https://msdn.microsoft.com/library/windows/hardware/ff541945)

[**dprintf**](https://msdn.microsoft.com/library/windows/hardware/ff542750)

[**GetExpression**](https://msdn.microsoft.com/library/windows/hardware/ff546683)

[**GetExpressionEx**](https://msdn.microsoft.com/library/windows/hardware/ff546691)

[**GetInputLine**](https://msdn.microsoft.com/library/windows/hardware/ff546905)

[**Ioctl**](https://msdn.microsoft.com/library/windows/hardware/ff551084)

[**GetKdContext**](https://msdn.microsoft.com/library/windows/hardware/ff546962)

[**ReadMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554287)

[**SearchMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554742)

[**WriteMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561420)

[**ReadMsr**](https://msdn.microsoft.com/library/windows/hardware/ff554289)

[**WriteMsr**](https://msdn.microsoft.com/library/windows/hardware/ff561424)

[**GetPebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff548122)

[**ReadPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff554310)

[**ReadPhysicalWithFlags**](https://msdn.microsoft.com/library/windows/hardware/ff554315)

[**WritePhysical**](https://msdn.microsoft.com/library/windows/hardware/ff561432)

[**WritePhysicalWithFlags**](https://msdn.microsoft.com/library/windows/hardware/ff561448)

[**GetTebAddress**](https://msdn.microsoft.com/library/windows/hardware/ff549267)

[**スタック トレース**](https://msdn.microsoft.com/library/windows/hardware/ff558794)

[**GetSymbol**](https://msdn.microsoft.com/library/windows/hardware/ff548447)

[**ReloadSymbols**](https://msdn.microsoft.com/library/windows/hardware/ff554381)

[**GetSetSympath**](https://msdn.microsoft.com/library/windows/hardware/ff548291)

[**TranslateVirtualToPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff558914)

Wdbgexts.h ヘッダー ファイルには、次の関数のプロトタイプが含まれています。 これらの関数では、32 ビットおよび 64 ビットの拡張機能のさまざまなプロトタイプを用意します。

[**ReadControlSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553527)

[**ReadControlSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553532)

[**ReadTypedControlSpace32**](https://msdn.microsoft.com/library/windows/hardware/ff554339)

[**ReadTypedControlSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff554341)

[**WriteControlSpace**](https://msdn.microsoft.com/library/windows/hardware/ff561375)

[**ReadIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff553574)

[**ReadIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff553577)

[**ReadIoSpaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff553580)

[**ReadIoSpaceEx64**](https://msdn.microsoft.com/library/windows/hardware/ff553583)

[**WriteIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff561406)

[**WriteIoSpace64**](https://msdn.microsoft.com/library/windows/hardware/ff561408)

[**WriteIoSpaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff561413)

[**WriteIoSpaceEx64**](https://msdn.microsoft.com/library/windows/hardware/ff561414)

[**SetThreadForOperation**](https://msdn.microsoft.com/library/windows/hardware/ff556830)

[**SetThreadForOperation64**](https://msdn.microsoft.com/library/windows/hardware/ff556832)

Wdbgexts.h ヘッダー ファイルには、次の関数のプロトタイプが含まれています。 これらの関数は、64 ビットの拡張機能でのみ使用できます。

[**GetFieldData**](https://msdn.microsoft.com/library/windows/hardware/ff546743)

[**GetFieldOffset**](https://msdn.microsoft.com/library/windows/hardware/ff546758)

[**GetFieldValue**](https://msdn.microsoft.com/library/windows/hardware/ff546781)

[**GetShortField**](https://msdn.microsoft.com/library/windows/hardware/ff548299)

[**ReadField**](https://msdn.microsoft.com/library/windows/hardware/ff553539)

[**ReadListEntry**](https://msdn.microsoft.com/library/windows/hardware/ff553585)

[**ReadPointer**](https://msdn.microsoft.com/library/windows/hardware/ff554318)

[**WritePointer**](https://msdn.microsoft.com/library/windows/hardware/ff561450)

[**IsPtr64**](https://msdn.microsoft.com/library/windows/hardware/ff551094)

[**ReadPtr**](https://msdn.microsoft.com/library/windows/hardware/ff554330)

[**GetTypeSize**](https://msdn.microsoft.com/library/windows/hardware/ff549446)

[**InitTypeRead**](https://msdn.microsoft.com/library/windows/hardware/ff550953)

[**InitTypeReadPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff550957)

[**ListType**](https://msdn.microsoft.com/library/windows/hardware/ff551988)

 

 





