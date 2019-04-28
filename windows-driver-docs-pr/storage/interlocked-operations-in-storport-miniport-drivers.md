---
title: Storport ミニポート ドライバーのインタロックされた操作
description: Windows アプリケーションで使用できるインター ロックされた関数の多くは、Storport ミニポート ドライバーでの使用に適しています。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec536bee0a57597da45cb2b1482a15e23f458ec6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368766"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport ミニポート ドライバーのインタロックされた操作


Windows アプリケーションで使用できるインター ロックされた関数の多くは、Storport ミニポート ドライバーでの使用に適しています。 これらの関数のほとんどは、コンパイラの組み込み関数として実装されておりは保護されている値の変更を同期するために適しています。

次のインタロックされた関数は、ミニポート ドライバーで使用できます。

**注**  で関数が宣言されている*miniport.h*または 32 ビット (x86) ドライバーで*storport.h*します。 プラットフォーム ソフトウェア開発キット (SDK) ドキュメントから関数の各トピックでは、使用状況の参照のみです。

 

## <a name="span-idinterlockedlogicalspanspan-idinterlockedlogicalspanlogical"></a><span id="interlocked_logical"></span><span id="INTERLOCKED_LOGICAL"></span>論理


[**InterlockedAnd**](https://msdn.microsoft.com/library/windows/desktop/ms683516)  
[**InterlockedAnd16**](https://msdn.microsoft.com/library/windows/desktop/ms683518)  
[**InterlockedAnd64**](https://msdn.microsoft.com/library/windows/desktop/ms683527)  
[**InterlockedOr**](https://msdn.microsoft.com/library/windows/desktop/ms683626)  
[**InterlockedOr16**](https://msdn.microsoft.com/library/windows/desktop/ms683627)  
[**InterlockedOr64**](https://msdn.microsoft.com/library/windows/desktop/ms683633)  
[**InterlockedXor**](https://msdn.microsoft.com/library/windows/desktop/ms684021)  
[**InterlockedXor16**](https://msdn.microsoft.com/library/windows/desktop/ms684024)  
[**InterlockedXor64**](https://msdn.microsoft.com/library/windows/desktop/ms684104)  
## <a name="span-idinterlockedassignmentspanspan-idinterlockedassignmentspanassignment"></a><span id="interlocked_assignment"></span><span id="INTERLOCKED_ASSIGNMENT"></span>割り当て


[**InterlockedExchange**](https://msdn.microsoft.com/library/windows/desktop/ms683590)  
[**InterlockedExchange64**](https://msdn.microsoft.com/library/windows/desktop/ms683593)  
[**InterlockedExchangePointer**](https://msdn.microsoft.com/library/windows/desktop/ms683609)  
## <a name="span-idinterlockedcomparisonspanspan-idinterlockedcomparisonspancomparison"></a><span id="interlocked_comparison"></span><span id="INTERLOCKED_COMPARISON"></span>比較


[**InterlockedCompareExchange**](https://msdn.microsoft.com/library/windows/desktop/ms683560)  
**InterlockedCompareExchange16**  
[**InterlockedCompareExchange64**](https://msdn.microsoft.com/library/windows/desktop/ms683562)  
[**InterlockedCompareExchangePointer**](https://msdn.microsoft.com/library/windows/desktop/ms683568)  
## <a name="span-idinterlockedarithmeticspanspan-idinterlockedarithmeticspanarithmetic"></a><span id="interlocked_arithmetic"></span><span id="INTERLOCKED_ARITHMETIC"></span>算術演算子


[**InterlockedDecrement**](https://msdn.microsoft.com/library/windows/desktop/ms683580)  
[**InterlockedDecrement64**](https://msdn.microsoft.com/library/windows/desktop/ms683581)  
[**InterlockedExchangeAdd**](https://msdn.microsoft.com/library/windows/desktop/ms683597)  
[**InterlockedExchangeAdd64**](https://msdn.microsoft.com/library/windows/desktop/ms683599)  
[**InterlockedIncrement**](https://msdn.microsoft.com/library/windows/desktop/ms683614)  
[**InterlockedIncrement64**](https://msdn.microsoft.com/library/windows/desktop/ms683615)  
 

 




