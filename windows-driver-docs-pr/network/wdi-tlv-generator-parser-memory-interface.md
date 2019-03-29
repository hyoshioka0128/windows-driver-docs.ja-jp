---
title: WDI TLV ジェネレーター/パーサー メモリ インターフェイス
description: パーサーとジェネレーター/削除を新しい C++ を内部的に使用します。
ms.assetid: 318519FF-AF1F-4D86-96A9-ED0918D91310
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50a22edbd4e4ee495ea517e82dcdf0255f01a95
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349807"
---
# <a name="wdi-tlv-generatorparser-memory-interface"></a>WDI TLV ジェネレーター/パーサー メモリ インターフェイス


パーサーとジェネレーター/削除を新しい C++ を内部的に使用します。 これには、いくつかの実装の詳細が簡略化します。 つまり、ライブラリのコンシューマーも、ライブラリにリンクするときに、これらの Api のオーバー ロードされた演算子の実装を提供する必要があります。 これは、コードが行う必要のある唯一の C++ 依存関係です。

割り当てを行うすべての Api は、パラメーターを受け取る*コンテキスト*PCTLV として型指定された\_を 2 つのフィールドを持つコンテキスト: ULONG\_という名前の PTR **AllocationContext**とという名前のULONG**PeerVersion**します。 **AllocationContext**フィールドは、オーバー ロードに渡す`new`演算子。 これにより、さまざまな方法で割り当てをカスタマイズする Api のコンシューマーができます。 詳細については、TLV\_コンテキスト パラメーターを参照してください[WDI TLV バージョン管理](wdi-tlv-versioning.md)。

**警告**  がするを (FreeParsed、CleanupParsed、FreeGenerated など)、ライブラリのクリーンアップ ルーチンの呼び出しをスキップしたくなる場合があります、それらの呼び出しは省略しないでください。 いくつかのコード パスで動作する可能性がありますが、診断ハードのメモリ リークになります。

 

ここでは、サンプルのオーバー ロードされた演算子です。

```C++
/*++
Module Name:
    sample.cpp
Abstract:
    Contains sample code to override C++ new/delete for use with TLV parser/generator library
Environment:
    Kernel mode
--*/
#include "precomp.h"

#define TLV_POOL_TAG (ULONG) '_VLT'

void* __cdecl operator new(size_t Size, ULONG_PTR AllocationContext)
/*++
  Override C++ allocation operator.
--*/
{
    PVOID pData = ExAllocatePoolWithTag(NonPagedPoolNx, Size, TLV_POOL_TAG);
    UNREFERENCED_PARAMETER(AllocationContext);
    if (pData != NULL)
    {
        RtlZeroMemory( pData, Size);
    }
    return pData;
} 

void __cdecl operator delete(void* pData)
/*++
  Override C++ delete operator.
--*/
{
    if (pData != NULL)
    {
        ExFreePoolWithTag(pData, TLV_POOL_TAG);
    }
}
```

 

 





