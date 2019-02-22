---
title: _Kernel_IoGetDmaAdapter_ドライバーの注釈
description: 使用して、 _Kernel_IoGetDmaAdapter_ DMA ポインターの誤用を検索するコード分析ツールに出力するための注釈。
ms.assetid: 51F71815-D899-48F5-8F81-92B139FC6B8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daa3e56cdfd451749b45dfb6dd360249c5f03db7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557949"
---
# <a name="kerneliogetdmaadapter-annotation-for-drivers"></a>\_カーネル\_IoGetDmaAdapter\_ドライバーの注釈


使用して、\_カーネル\_IoGetDmaAdapter\_ DMA ポインターの誤用を検索するコード分析ツールに出力するための注釈。

関数は、注釈が付けられたインターフェイスを呼び出す場合、\_カーネル\_IoGetDmaAdapter\_注釈、関数が成功するまでに発生した再試行などの再試行ロジックがその必要があります。

IoGetDmaAdapter ルーチンは、レジスタの要求の数よりも少ないを返すことができ、呼び出し元が実際の数を使用して実行するために必要な要求の数ではありません。

```ManagedCPlusPlus
_Must_inspect_result_
_IRQL_requires_max_(PASSIVE_LEVEL)
NTKERNELAPI
struct _DMA_ADAPTER *
IoGetDmaAdapter(
    _In_opt_ PDEVICE_OBJECT PhysicalDeviceObject,           // required for PnP drivers
    _In_ struct _DEVICE_DESCRIPTION *DeviceDescription,
    _Out_ _When_(return!=0, _Kernel_IoGetDmaAdapter_ _At_(*NumberOfMapRegisters, _Must_inspect_result_))
    PULONG NumberOfMapRegisters
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SAL 2.0 Annotations for Windows Drivers](sal-2-annotations-for-windows-drivers.md)

 

 






