---
title: WDM ドライバーでの浮動小数点の使用
description: Windows 用のカーネルモード WDM ドライバーは、浮動小数点演算を使用するときに特定のガイドラインに従う必要があります。 これらは、x86 システムと x64 システムで異なります。 既定では、Windows は両方のシステムの算術例外をオフにします。
ms.assetid: 73414084-4054-466a-b64c-5c81b224be92
keywords:
- 浮動小数点 WDK カーネル
- 浮動小数点単位の WDK カーネル
- FPU WDK カーネル
- Kesaveflo/Pointstate
- Kerestoreflo/Pointstate
- WDM ドライバー WDK カーネル、浮動小数点演算
- MMX WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4177a3d8552e84f228e48119fe29405b8d98032f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835993"
---
# <a name="using-floating-point-in-a-wdm-driver"></a>WDM ドライバーでの浮動小数点の使用


**最終更新日**

-   2016 年 7 月

Windows 用のカーネルモード WDM ドライバーは、浮動小数点演算を使用するときに特定のガイドラインに従う必要があります。 これらは、x86 システムと x64 システムで異なります。 既定では、Windows は両方のシステムの算術例外をオフにします。

## <a name="x86-systems"></a>x86 システム


X86 システム用のカーネルモード WDM ドライバーでは、 [**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)と[**Kerestoreextendedprocessorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)の呼び出しの間で、浮動小数点の計算の使用をラップする必要があります。 浮動小数点演算は、コンパイラの並べ替えによって**KeSaveExtendedProcessorState**の戻り値をチェックする前に、浮動小数点の計算が実行されないようにするために、非インラインのサブルーチンに配置する必要があります。

コンパイラは、このような計算に対して、浮動小数点ユニット (FPU) レジスタとも呼ばれる MMX/x87 を使用します。このような計算は、ユーザーモードアプリケーションで同時に使用することができます。 これらのレジスタを使用する前に保存しなかった場合、または完了時に復元できなかった場合は、アプリケーションで計算エラーが発生する可能性があります。

X86 システムのドライバーは、 [**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)を呼び出し、IRQL &lt;= ディスパッチ\_レベルで浮動小数点演算を実行できます。 浮動小数点演算は、x86 システム上の割り込みサービスルーチン (Isr) ではサポートされていません。

## <a name="x64-systems"></a>x64 システム


64ビットコンパイラでは、浮動小数点演算に MMX/x87 レジスタは使用されません。 代わりに、SSE レジスタを使用します。 x64 カーネルモードコードは MMX/x87 レジスタへのアクセスが許可されていません。 また、コンパイラは SSE 状態を適切に保存して復元します。したがって、 [**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)と[**Kerestoreextendedprocessorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)の呼び出しは不要で、浮動小数点演算を isr で使用できます。 AVX などの他の拡張プロセッサ機能を使用するには、拡張された状態を保存および復元する必要があります。 詳細については、「 [Windows ドライバーでの拡張プロセッサ機能の使用](floating-point-support-for-64-bit-drivers.md)」を参照してください。

## <a name="example"></a>例


次の例は、WDM ドライバーが FPU アクセスをラップする方法を示しています。

```cpp
__declspec(noinline)
VOID
DoFloatingPointCalculation(
    VOID
    )
{
    double Duration;
    LARGE_INTEGER Frequency;

    Duration = 1000000.0;
    DbgPrint("%I64x\n", *(LONGLONG*)&Duration);
    KeQueryPerformanceCounter(&Frequency);
    Duration /= (double)Frequency.QuadPart;
    DbgPrint("%I64x\n", *(LONGLONG*)&Duration);
}

NTSTATUS
DriverEntry(
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{

    XSTATE_SAVE SaveState;
    NTSTATUS Status;

    Status = KeSaveExtendedProcessorState(XSTATE_MASK_LEGACY, &SaveState);
    if (!NT_SUCCESS(Status)) {
        goto exit;
    }

    __try {
        DoFloatingPointCalculation();
    }
    __finally {
        KeRestoreExtendedProcessorState(&SaveState);
    }

exit:
    return Status;
}
```

この例では、浮動小数点変数への代入は、 [**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)と[**Kerestoreextendedprocessorstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestoreextendedprocessorstate)の呼び出しの間で行われます。 浮動小数点変数への代入では FPU が使用されるため、ドライバーは、このような変数を初期化する前に、 **KeSaveExtendedProcessorState**がエラーなしで返されたことを確認する必要があります。

前の呼び出しは x64 システムでは不要であり、XSTATE\_MASK\_レガシフラグが指定されている場合は無害です。 そのため、x64 システムのドライバーをコンパイルするときに、コードを変更する必要はありません。

X86 ベースのシステムでは、 [**KeSaveExtendedProcessorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesaveextendedprocessorstate)から戻ったときに、FNINIT の呼び出しによって FPU が既定の状態にリセットされます。

 

 




