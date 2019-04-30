---
title: WDM ドライバーでの浮動小数点の使用
description: 浮動小数点演算を使用する場合、Windows のカーネル モード WDM ドライバーは特定のガイドラインに従う必要があります。 これらは、x86 および x64 システムによって異なります。 既定では、Windows は、両方のシステムの算術例外をオフにします。
ms.assetid: 73414084-4054-466a-b64c-5c81b224be92
keywords:
- 浮動小数点のポイントの WDK カーネル
- 浮動小数点ユニットの WDK カーネル
- FPU WDK カーネル
- KeSaveFloatingPointState
- KeRestoreFloatingPointState
- WDM ドライバー WDK カーネル、浮動小数点演算
- MMX WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6235167e1d91c94fa3d9c60f6f1dc50eb3d4a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387403"
---
# <a name="using-floating-point-in-a-wdm-driver"></a>WDM ドライバーでの浮動小数点の使用


**最終更新日**

-   2016 年 7 月

浮動小数点演算を使用する場合、Windows のカーネル モード WDM ドライバーは特定のガイドラインに従う必要があります。 これらは、x86 および x64 システムによって異なります。 既定では、Windows は、両方のシステムの算術例外をオフにします。

## <a name="x86-systems"></a>x86 システム


X86 システムは、浮動小数点計算への呼び出しの間での使用をラップする必要がありますのカーネル モード WDM ドライバー [ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)と[ **KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)します。 浮動小数点演算は、浮動小数点演算がの戻り値をチェックする前に実行しないことを確認する非インライン サブルーチンに配置する必要があります**KeSaveExtendedProcessorState**コンパイラによる並べ替えのためです。

コンパイラは、MMX/x87 浮動小数点ユニット (FPU) の登録とも呼ばれるこのような計算では、ユーザー モード アプリケーションで同時に使用できるを使用します。 完了したら、それらを復元する、または失敗を使用する前にこれらのレジスタの保存に失敗したアプリケーションで計算エラーがあります。

システムを呼び出すことができます x86 用のドライバー [ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238) IRQL で浮動小数点演算の実行と&lt;= ディスパッチ\_レベル。 浮動小数点演算が x86 では、割り込みサービス ルーチン (Isr) でサポートされていないシステム。

## <a name="x64-systems"></a>x64 システム


64 ビット コンパイラでは、浮動小数点演算の/x87 MMX レジスタを使用しません。 代わりに、SSE レジスタを使用します。 x64/x87 MMX レジスタにアクセスするカーネル モード コードが許可されていません。 コンパイラも正しく保存の処理し、そのため、呼び出し、SSE 状態の復元[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)と[ **KeRestoreExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553182) isr を特定の操作を使用できる、不要なおよび浮動小数点のポイントします。 AVX などその他のプロセッサの拡張機能の使用、拡張状態の保存と復元が必要です。 詳細については、次を参照してください。 [Windows ドライバーでプロセッサ機能を拡張を使用して](floating-point-support-for-64-bit-drivers.md)します。

## <a name="example"></a>例


次の例では、WDM ドライバーが、FPU のアクセスをラップする方法を示しています。

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

例では、浮動小数点変数への代入はへの呼び出し間で行われます[ **KeSaveExtendedProcessorState** ](https://msdn.microsoft.com/library/windows/hardware/ff553238)と[ **KeRestoreExtendedProcessorState。**](https://msdn.microsoft.com/library/windows/hardware/ff553182). ドライバーを確認する必要があります浮動小数点変数に割り当てを使用して、FPU、ため**KeSaveExtendedProcessorState**がこのような変数を初期化する前にエラーが発生せず返されます。

前の呼び出しは、x64 不要システムと無害な場合に、XSTATE\_マスク\_レガシ フラグが指定されています。 そのため、x64 用のドライバーをコンパイルするときに、コードを変更する必要はありませんシステム。

X86 ベースのシステムでは、既定の状態に、FPU をリセット FNINIT への呼び出しから戻ったときで[ **KeSaveExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553238)します。

 

 




