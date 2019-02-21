---
title: 固定精度のデータ型の不整合を回避します。
description: 固定精度のデータ型の不整合を回避します。
ms.assetid: 4e214bd8-b622-447a-b484-bd1d5d239de7
keywords:
- WDK の 64 ビットのコードをファイル システムの制御
- FSCTL WDK 64 ビット
- 制御コード WDK 64 ビット
- I/O 制御コード WDK カーネル、64 ビット ドライバーで 32 ビットの I/O
- Ioctl WDK カーネルでは、64 ビット ドライバーで 32 ビットの I/O
- ポインターの精度を WDK の 64 ビット
- 固定精度のデータ型を WDK の 64 ビット
- 不整合の固定精度のデータ型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384f999800faef2e74e0252c0fdd3c6100cdd2f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532488"
---
# <a name="avoiding-misalignment-of-fixed-precision-data-types"></a>固定精度のデータ型の不整合を回避します。





残念ながら、データ型の同じサイズが 32 ビットおよび 64 ビット プログラミングのさまざまな配置要件があることができます。 そのため固定精度の型へのポインターの有効桁数のデータ型を変更することですべての IOCTL/FSCTL バッファー不整合の問題を回避できます。 つまり、カーネル モード ドライバーの Ioctl と FSCTLs 特定固定有効桁数のデータ型 (またはそれらへのポインター) を格納するバッファーを渡すこともできますが thunked する必要があります。

### <a name="which-data-types-are-affected"></a>どの種類のデータが影響を受ける

問題は、固定有効桁数のデータ型は構造体に影響します。 これは、構造体のアラインメント要件を決定するルールがプラットフォームに固有であるためです。

たとえば、  **\_ \_int64**大きな\_整数、および KFLOATING\_保存は x86 上で 4 バイト境界に合わせて調整する必要がありますプラットフォーム。 ただし、Itanium ベースのコンピューターにそれらは、8 バイト境界に合わせて調整する必要があります。

特定のプラットフォーム上の特定のデータ型のアラインメント要件を確認するのには、使用、**型\_配置**プラットフォームでのマクロ。

### <a name="how-to-fix-the-problem"></a>問題を解決するには、方法

IOCTL はメソッドを次の例で\_どちらの IOCTL のため、 **Irp -&gt;UserBuffer**カーネル モード ドライバーにユーザー モード アプリケーションから直接ポインターが渡されます。 Ioctl および FSCTLs で使用されるバッファーでは、検証は実行されません。 呼び出すための[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)または[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)バッファー ポインターは、安全に逆参照が必要です。

いると仮定すると、32 ビット アプリケーション有効な値に渡すことが**Irp -&gt;UserBuffer**、LARGE\_によって示される整数構造**p -&gt;DeviceTime**されます4 バイト境界上にアラインされます。 **ProbeForRead**で渡される値に対しては、この配置を確認します。 その*配置*パラメーターで、ここでは**型\_配置**(LARGE\_整数)。 X86 プラットフォームでは、このマクロの式は、4 (バイト単位) を返します。 ただし、Itanium ベースのマシンでは、上に 8 が返されます、原因**ProbeForRead**状態を発生させる\_DATATYPE\_の不整合例外。

**注**  削除して、 **ProbeForRead**呼び出しも、問題が解決しないが、のみと、診断が困難になります。

 

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

次のセクションでは、上記で説明した問題を解決する方法を説明します。 簡潔にするためのすべてのコード スニペットを編集したことに注意してください。

### <a name="solution-1-copy-the-buffer"></a>解決方法 1:バッファーにコピーします。

不整合の問題を回避するために最も安全な方法では、次の例のように、その内容にアクセスする前に、バッファーのコピーを作成します。

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

このソリューションは、バッファーの内容が正しく配置されているかどうかに、まず調べることによってパフォーマンスを向上させる最適化できます。 そうである場合は、バッファーが使用できます。 それ以外の場合、ドライバーは、バッファーのコピーを作成します。

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

### <a name="solution-2-use-the-unaligned-macro"></a>解決方法 2:アラインされていないマクロを使用します。

**整列されていない**マクロにアクセスできるコードを生成する C コンパイラに指示、 **DeviceTime**アラインメント エラーにすることがなくフィールド。 Itanium ベースのプラットフォームでこのマクロを使用して、ドライバーを大幅に拡大し、低速の可能性があるに注意してください。

```cpp
typedef struct _IOCTL_PARAMETERS2 {
    LARGE_INTEGER DeviceTime;
} IOCTL_PARAMETERS2;
typedef IOCTL_PARAMETERS2 UNALIGNED *PIOCTL_PARAMETERS2;
```

### <a name="pointers-are-also-affected"></a>ポインターも影響を受けます

前に説明した、不整合の問題は、バッファー内の I/O 要求でも発生することができます。 次の例では、IOCTL バッファーには大規模に埋め込みのポインターが含まれています\_整数構造体。

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;0

#define COUNT_FUNCTION 1
#define IOCTL_GETCOUNT CTL_CODE(FILE_DEVICE_UNKNOWN, \
            COUNT_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

メソッドのような\_も IOCTL と FSCTL バッファー ポインターの前に説明した、カーネル モード ドライバーにユーザー モード アプリケーションから直接 I/O 要求をバッファー内に埋め込まれているポインターが渡されるもします。 これらのポインターでは、検証は実行されません。 呼び出すための[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)または[ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)で囲まれている、**試用/を除く**ブロック、埋め込みポインターを安全に逆参照する前に必要です。

32 ビット アプリケーションが有効な値に成功したと仮定すると、前の例のように**pDeviceCount**、LARGE、\_によって示される整数構造**pDeviceCount** 4 - 上に配置されバイトの境界。 **ProbeForRead**と**ProbeForWrite**の値に対しては、この配置の確認、*配置*型をここでは、パラメーター\_配置 (LARGE\_整数)。 X86 プラットフォームでは、このマクロの式は、4 (バイト単位) を返します。 ただし、Itanium ベースのマシンでは、上に 8 が返されます、原因**ProbeForRead**または**ProbeForWrite**状態を発生させる\_DATATYPE\_の不整合例外。

適切に配置された、LARGE のコピーを作成してこの問題を解決できます\_整数構造体、または次のようにアラインされていないマクロを使用して、ソリューションの 1 のようにします。

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER UNALIGNED *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;
```

 

 




