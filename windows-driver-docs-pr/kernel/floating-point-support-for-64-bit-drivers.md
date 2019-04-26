---
title: Windows ドライバーでの拡張プロセッサ機能の使用
description: X86 および x64 のシステム プロセッサの拡張機能を使用する Windows ドライバーは、同時実行アプリケーションのエラーを回避するために、KeSaveExtendedProcessorState への呼び出しと KeRestoreExtendedProcessorState 間の浮動小数点演算をラップする必要がありますが使用して、レジスタ。
ms.assetid: a42e86cf-47a2-44ed-8bf1-7407633af8b7
keywords:
- 浮動小数点のポイントの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1f893e4917e3bb82e091ae372b017f7cf11f14f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359951"
---
# <a name="using-extended-processor-features-in-windows-drivers"></a>Windows ドライバーでの拡張プロセッサ機能の使用


**最終更新日**

-   2016 年 7 月

X86 および x64 のシステム プロセッサの拡張機能を使用する Windows ドライバーは、呼び出しの間で浮動小数点演算をラップする必要があります[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)と[ **KeRestoreExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553182)レジスタを使用して同時実行アプリケーションでエラーを回避するためにします。

## <a name="legacy-mmxx87-registers"></a>レガシ MMX/x87 レジスタ


これらのレジスタは、XSTATE に対応して\_マスク\_レガシ\_浮動\_ポイント マスクと x64 用のドライバーが利用できないシステム。 これらの詳細についてを参照してくださいを登録の[WDM ドライバーで使用する浮動小数点](using-floating-point-or-mmx-in-a-wdm-driver.md)します。

## <a name="sse-registers"></a>SSE レジスタ


これらのレジスタは、XSTATE に対応\_マスク\_レガシ\_SSE フラグとは、x64 で使用される浮動小数点演算のコンパイラ。 これらのレジスタを使用するシステムする必要があります保存に使用する前に、XSTATE を渡すことで x86 用のドライバー\_マスク\_レガシまたは XSTATE\_マスク\_レガシ\_SSE フラグ、 [ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)呼び出しを完了したら、それらを復元[ **KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)します。 X64 では必要でないシステムでは、有害なされませんが。 これらの詳細についてを参照してくださいを登録の[WDM ドライバーで使用する浮動小数点](using-floating-point-or-mmx-in-a-wdm-driver.md)します。

## <a name="avx-registers"></a>AVX レジスタ


これらのレジスタは、XSTATE に対応して\_マスク\_GSSE または XSTATE\_マスク\_AVX マスク。 新しい x86 など、Intel Sandy Bridge (旧称 Gesher) プロセッサのプロセッサが AVX 命令をサポートし、セット (YMM0 YMM15) を登録します。 Service Pack 1 (SP1)、Windows Server 2008 R2 では、新しいバージョンの Windows と Windows 7 では、x86 と x64 の両方のバージョンのオペレーティング システムは、AVX スレッド (とプロセス) の間でのレジスタのスイッチを保持します。 AVX レジスタをカーネル モードで使用するには、ドライバー (x86 および x64) が明示的に保存して AVX レジスタを復元する必要があります。 AVX レジスタは、割り込みサービス ルーチンでは使用できませんし、算術例外は既定でオフにします。

```cpp
include ksamd64.inc

        subttl "Set YMM State."
;++
;
; Routine Description:
;   
;   This routine loads the first four YMM registers with the state supplied.
;
; Arguments;
;
;   rcx - Supplies a pointer to the values we want to load.
;
; Return Value:
;
;   None
;
;--

LEAF_ENTRY SetYmmValues, _TEXT$00

        vmovdqa    ymm0,  ymmword ptr[rcx + 0]
        vmovdqa    ymm1,  ymmword ptr[rcx + 32]
        vmovdqa    ymm2,  ymmword ptr[rcx + 64]
        vmovdqa    ymm3,  ymmword ptr[rcx + 96]

        ret

LEAF_END SetYmmValues, _TEXT$00

        end
```

```cpp
typedef DECLSPEC_ALIGN(32) struct _YMM_REGISTERS {
    ULONG64 Ymm4Registers[16];
} YMM_REGISTERS, *PYMM_REGISTERS;

VOID
FASTCALL
SetYmmValues(
    __in PYMM_REGISTERS YmmRegisterValues
    );

NTSTATUS
DriverEntry (
    __in PDRIVER_OBJECT DriverObject,
    __in PUNICODE_STRING RegistryPath
    )
{

    NTSTATUS Status;
    XSTATE_SAVE SaveState;
    ULONG64 EnabledFeatures;

    //
    // Load the first 4 YMM registers as 4 vectors of 4 64-bit integers.
    //

    YMM_REGISTERS RegisterValues = { 0, 1, 2, 3,        // YMM0
                                     4, 5, 6, 7,        // YMM1
                                     8, 9, 10, 11,      // YMM2
                                     12, 13, 14, 15 };  // YMM3

    //
    // Check to see if AVX is available. Bail if it is not.
    //

    EnabledFeatures = RtlGetEnabledExtendedFeatures(-1);
    if ((EnabledFeatures & XSTATE_MASK_GSSE) == 0) {
        Status = STATUS_FAILED_DRIVER_ENTRY;
        goto exit;
    }

    Status = KeSaveExtendedProcessorState(XSTATE_MASK_GSSE, &SaveState);

    if (!NT_SUCCESS(Status)) {
        goto exit;
    }

    __try {
        SetYmmValues(&RegisterValues);
    }
    __finally {
        KeRestoreExtendedProcessorState(&SaveState);
    }

exit:
    return Status;
}
```

## <a name="related-topics"></a>関連トピック
[**KeSaveExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553238)  
[**KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)  
[WDM ドライバーでの浮動小数点を使用してください。](using-floating-point-or-mmx-in-a-wdm-driver.md)  



