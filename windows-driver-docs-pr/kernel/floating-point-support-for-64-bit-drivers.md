---
title: Windows ドライバーでの拡張プロセッサ機能の使用
description: 拡張プロセッサ機能を使用する x86 および x64 システム用の Windows ドライバーでは、同時実行アプリケーションのエラーを回避するために、KeSaveExtendedProcessorState と KeRestoreExtendedProcessorState の呼び出しの間で浮動小数点の計算をラップする必要があります。レジスタを使用している可能性があります。
ms.assetid: a42e86cf-47a2-44ed-8bf1-7407633af8b7
keywords:
- 浮動小数点 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49b735b9eb8b578b0554a77e241b0b246945e1dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838690"
---
# <a name="using-extended-processor-features-in-windows-drivers"></a>Windows ドライバーでの拡張プロセッサ機能の使用


**最終更新日時**

-   2016 年 7 月

拡張プロセッサ機能を使用する x86 および x64 システム用の Windows ドライバーは、同時に発生するエラーを回避するために、 [**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)と[**Kerestoreextendedprocessorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)の呼び出しの間で浮動小数点の計算をラップする必要があります。レジスタを使用している可能性のあるアプリケーション。

## <a name="legacy-mmxx87-registers"></a>レガシ MMX/x87 レジスタ


これらのレジスタは、XSTATE\_MASK\_レガシ\_浮動\_ポイントマスクに対応しており、x64 システムのドライバーでは使用できません。 これらのレジスタの詳細については[、「WDM ドライバーでの浮動小数点の使用](using-floating-point-or-mmx-in-a-wdm-driver.md)」を参照してください。

## <a name="sse-registers"></a>SSE レジスタ


これらのレジスタは、XSTATE\_MASK\_レガシ\_SSE フラグに対応し、浮動小数点演算のために x64 コンパイラによって使用されます。 これらのレジスタを使用する x86 システムのドライバーは、XSTATE\_マスク\_レガシまたは XSTATE\_マスクを渡すことによって、 [**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)呼び出しのレガシ\_SSE フラグ\_、完了したときに、それらを保存する必要があります。[**Kerestoreextendedprocessorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)を使用して復元します。 これは x64 システムでは不要ですが、害はありません。 これらのレジスタの詳細については[、「WDM ドライバーでの浮動小数点の使用](using-floating-point-or-mmx-in-a-wdm-driver.md)」を参照してください。

## <a name="avx-registers"></a>AVX レジスタ


これらのレジスタは、XSTATE\_MASK\_GSSE または XSTATE\_MASK\_AVX マスクに対応します。 Intel Sandy Bridge (旧称 Gesher) プロセッサなどの新しい x86 プロセッサは、AVX 命令と register set (YMM0 ~ YMM5-YMM15) をサポートしています。 Windows 7 Service Pack 1 (SP1)、Windows Server 2008 R2、およびそれ以降のバージョンの Windows では、x86 と x64 の両方のバージョンのオペレーティングシステムで、スレッド (およびプロセス) のスイッチ間で AVX レジスタが保持されます。 カーネルモードで AVX レジスタを使用するには、ドライバー (x86 および x64) が AVX レジスタを明示的に保存および復元する必要があります。 AVX レジスタは、割り込みサービスルーチンでは使用できません。また、算術例外は既定で無効になっています。

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
[**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)  
[**KeRestoreExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)  
[WDM ドライバーでの浮動小数点の使用](using-floating-point-or-mmx-in-a-wdm-driver.md)  



