---
title: IRP ベースの IOCTL と FSCTL 操作
description: IRP ベースの IOCTL と FSCTL 操作
ms.assetid: 08d6cf89-aaba-4aa1-baff-eb6aece2875f
keywords:
- WDK の Ioctl ファイル システム
- FSCTL WDK ファイル システム
- WDK のバッファーにファイル システムがありません。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1106fef7d2c48024f28dc2a33136545a853fb0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384567"
---
# <a name="irp-based-ioctl-and-fsctl-operations"></a>IRP ベースの IOCTL と FSCTL 操作


## <span id="ddk_irp_based_ioctl_and_fsctl_operations_if"></span><span id="DDK_IRP_BASED_IOCTL_AND_FSCTL_OPERATIONS_IF"></span>


次の IRP ベースの I/O 操作では、I/O 制御コード (IOCTL) またはファイル システムの制御コード (FSCTL) の定義で指定されている転送の種類に一致するバッファリング メソッドを使用します。

-   IRP\_MJ\_DEVICE\_CONTROL

-   IRP\_MJ\_ファイル\_システム\_コントロール

-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL

転送の種類がで指定された、 *TransferType*パラメーターは、CTL の\_コード マクロ。 特定の IOCTL または FSCTL 転送の種類を取得するには、次のマクロを使用します。

```cpp
#define METHOD_FROM_CTL_CODE(ctrlCode)         ((ULONG)(ctrlCode & 3))
```

このマクロは、次の値のいずれかを返します。

```cpp
#define METHOD_BUFFERED                 0
#define METHOD_IN_DIRECT                1
#define METHOD_OUT_DIRECT               2
#define METHOD_NEITHER                  3
```

詳細については、CTL\_マクロのコードは、「 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)します。

注その IRP\_MJ\_デバイス\_コントロールは高速な I/O 操作にもできます。 高速な I/O 操作である場合は、IOCTL の転送の種類に関係なく、バッファーも直接 I/O が常に使用します。 タイミングの詳細については IRP\_MJ\_デバイス\_コントロールが高速な I/O 操作を参照してください[操作することができますが IRP ベースまたは高速の I/O](operations-that-can-be-irp-based-or-fast-i-o.md)します。

 

 




