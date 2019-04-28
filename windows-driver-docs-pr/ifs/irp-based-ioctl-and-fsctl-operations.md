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
ms.openlocfilehash: 73cbfd8855a3481090d997b436f5d80d36dd1c84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379716"
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

詳細については、CTL\_マクロのコードは、「 [I/O 制御コードを定義する](https://msdn.microsoft.com/library/windows/hardware/ff543023)します。

注その IRP\_MJ\_デバイス\_コントロールは高速な I/O 操作にもできます。 高速な I/O 操作である場合は、IOCTL の転送の種類に関係なく、バッファーも直接 I/O が常に使用します。 タイミングの詳細については IRP\_MJ\_デバイス\_コントロールが高速な I/O 操作を参照してください[操作することができますが IRP ベースまたは高速の I/O](operations-that-can-be-irp-based-or-fast-i-o.md)します。

 

 




