---
title: 精度が固定されているデータ型の不整合回避
description: 精度が固定されているデータ型の不整合回避
ms.assetid: 4e214bd8-b622-447a-b484-bd1d5d239de7
keywords:
- ファイルシステム制御コード WDK 64 ビット
- FSCTL WDK 64-bit
- コントロールコード WDK 64-bit
- I/o 制御コード WDK カーネル、64ビットドライバーでの32ビット i/o
- Ioctl WDK カーネル、64ビットドライバーの32ビット i/o
- ポインターの有効桁数 WDK 64-bit
- 固定精度データ型 WDK 64 ビット
- 固定精度のデータ型の不整合
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9fcd0eb33b92456e51f4e048b0f5e47666659a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837177"
---
# <a name="avoiding-misalignment-of-fixed-precision-data-types"></a>精度が固定されているデータ型の不整合回避





残念ながら、32ビットおよび64ビットのプログラミングでは、データ型のサイズは同じですが、アラインメント要件が異なる可能性があります。 したがって、ポインターの有効桁数のデータ型を固定精度の型に変更することで、IOCTL/FSCTL バッファーの不整合の問題を回避することはできません。 これは、特定の固定精度データ型 (またはポインターへのポインター) を含むバッファーを渡すカーネルモードドライバーの Ioctl と FSCTLs も、thunked である必要があることを意味します。

### <a name="which-data-types-are-affected"></a>影響を受けるデータ型

この問題は、それ自体が構造体である固定精度データ型に影響します。 これは、構造体の配置要件を決定するための規則がプラットフォーム固有であるためです。

たとえば、 **\_\_int64**、LARGE\_INTEGER、および kfloating\_SAVE は、x86 プラットフォームの4バイト境界でアラインする必要があります。 ただし、Itanium ベースのコンピューターでは、8バイトの境界上に配置する必要があります。

特定のプラットフォームの特定のデータ型のアラインメント要件を判断するには、そのプラットフォームで**型\_アラインメント**マクロを使用します。

### <a name="how-to-fix-the-problem"></a>問題を解決する方法

次の例では、IOCTL は IOCTL\_メソッドではないため、 **Irp&gt;の UserBuffer**ポインターはユーザーモードアプリケーションからカーネルモードドライバーに直接渡されます。 Ioctl および FSCTLs で使用されるバッファーに対しては、検証は実行されません。 したがって、バッファーポインターを安全に逆参照するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)または[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)を呼び出す必要があります。

32ビットアプリケーションが**Irp&gt;UserBuffer**の有効な値を渡したと仮定した場合、 **p&gt;DEVICETIME**が指す大きな\_整数構造体は、4バイトの境界に配置されます。 **ProbeForRead** *は、アラインメントパラメーターで*渡された値に対してこの配置を確認します。この例では、**型\_アラインメント**(LARGE\_INTEGER) です。 X86 プラットフォームでは、このマクロ式は 4 (バイト) を返します。 ただし、Itanium ベースのコンピューターでは8が返され、 **ProbeForRead**によって\_データ型\_不整合例外の状態が発生します。

**ProbeForRead**の呼び出しを削除しても問題は解決されませんが、診断が難しくなるだけです **。  **

 

```cpp
typedef struct _IOCTL_PARAMETERS2 {
    LARGE_INTEGER DeviceTime;
} IOCTL_PARAMETERS2, *PIOCTL_PARAMETERS2;

#define SETTIME_FUNCTION 1
#define IOCTL_SETTIME CTL_CODE(FILE_DEVICE_UNKNOWN, \
            SETTIME_FUNCTION, METHOD_NEITHER, FILE_ANY_ACCESS)

...

case IOCTL_SETTIME:
    PIOCTL_PARAMETERS2 p = (PIOCTL_PARAMETERS2)Irp->UserBuffer;

    try {                 
        if (Irp->RequestorMode != KernelMode) { 
            ProbeForRead ( p->DeviceTime,
                      sizeof( LARGE_INTEGER ),
                      TYPE_ALIGNMENT( LARGE_INTEGER ));
    }
    status = DoSomeWork(p->DeviceTime);

 } except( EXCEPTION_EXECUTE_HANDLER ) {
```

以下のセクションでは、上記の問題の解決方法について説明します。 すべてのコードスニペットが簡潔になるように編集されていることに注意してください。

### <a name="solution-1-copy-the-buffer"></a>解決策 1: バッファーをコピーする

不整合の問題を回避する最も安全な方法は、次の例のように、バッファーのコピーを作成してからその内容にアクセスすることです。

```cpp
case IOCTL_SETTIME: {
    PIOCTL_PARAMETERS2 p = (PIOCTL_PARAMETERS2)Irp->UserBuffer;
#if _WIN64
    IOCTL_PARAMETERS2 LocalParams2;

    RtlCopyMemory(&LocalParams2, p, sizeof(IOCTL_PARAMETERS2));
    p = &LocalParams2;
#endif

    status = DoSomeWork(p->DeviceTime);
    break;
}
```

このソリューションは、バッファーの内容が適切にアラインされているかどうかを最初に確認することで、パフォーマンスを向上させるために最適化できます。 その場合は、バッファーをそのように使用できます。 それ以外の場合は、ドライバーによってバッファーのコピーが作成されます。

```cpp
case IOCTL_SETTIME: {
    PIOCTL_PARAMETERS2 p = (PIOCTL_PARAMETERS2)Irp->UserBuffer;
#if _WIN64
    IOCTL_PARAMETERS2 LocalParams2;

    if ( (ULONG_PTR)p & (TYPE_ALIGNMENT(IOCTL_PARAMETERS2)-1)) {
        // The buffer contents are not correctly aligned for this 
        // platform, so copy them into a properly aligned local 
        // buffer.
        RtlCopyMemory(&LocalParams2, p, sizeof(IOCTL_PARAMETERS2));
        p = &LocalParams2;
    }
#endif

    status = DoSomeWork(p->DeviceTime);
    break;
}
```

### <a name="solution-2-use-the-unaligned-macro"></a>解決方法 2: 整列されていないマクロを使用する

整列**されていないマクロは**、アラインメントエラーを発生させることなく**devicetime**フィールドにアクセスできるコードを生成するように C コンパイラに指示します。 Itanium ベースのプラットフォームでこのマクロを使用すると、ドライバーのサイズが大幅に大きくなり、速度が低下する可能性があることに注意してください。

```cpp
typedef struct _IOCTL_PARAMETERS2 {
    LARGE_INTEGER DeviceTime;
} IOCTL_PARAMETERS2;
typedef IOCTL_PARAMETERS2 UNALIGNED *PIOCTL_PARAMETERS2;
```

### <a name="pointers-are-also-affected"></a>ポインターも影響を受けます。

前に説明した不整合の問題は、バッファーされた i/o 要求でも発生する可能性があります。 次の例では、IOCTL バッファーに、大きな\_整数構造体への埋め込みポインターが含まれています。

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;0

#define COUNT_FUNCTION 1
#define IOCTL_GETCOUNT CTL_CODE(FILE_DEVICE_UNKNOWN, \
            COUNT_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

メソッドと同様に、前に説明した IOCTL および FSCTL バッファーポインターのいずれ\_も、バッファー i/o 要求に埋め込まれているポインターは、ユーザーモードアプリケーションからカーネルモードドライバーに直接渡されます。 これらのポインターに対して検証は実行されません。 したがって、埋め込みポインターを安全に逆参照するには、 **try/except**ブロックで囲まれた[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)または[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)の呼び出しが必要です。

前の例と同様に、32ビットアプリケーションが**pdevicecount**の有効な値を渡していると仮定すると、 **PDEVICECOUNT**が指す大きな\_整数構造体は、4バイトの境界に配置されます。 **ProbeForRead**と**ProbeForWrite**アラインメントパラメーターの値に対してこの配置を確認します。この例では、型 *\_アラインメント (* LARGE\_INTEGER) です。 X86 プラットフォームでは、このマクロ式は 4 (バイト) を返します。 ただし、Itanium ベースのコンピューターでは8が返され、 **ProbeForRead**または**ProbeForWrite**はステータス\_DATATYPE\_ミスアライメント例外を発生させます。

この問題を解決するには、ソリューション1と同様に、大きな\_整数構造体の適切にアラインされたコピーを作成するか、または次のように整列されていないマクロを使用します。

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER UNALIGNED *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;
```

 

 




