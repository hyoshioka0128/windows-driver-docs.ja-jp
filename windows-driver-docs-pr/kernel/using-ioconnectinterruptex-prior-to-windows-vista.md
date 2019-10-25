---
title: Windows Vista より前の IoConnectInterruptEx の使用
description: Windows Vista より前の IoConnectInterruptEx の使用
ms.assetid: a08b2869-93f8-440b-9fbe-068604c6007d
keywords:
- IoConnectInterruptEx
- iointex .h
- 行ベースの割り込み (WDK カーネル)
- メッセージシグナル割り込み (WDK カーネル)
- CONNECT_LINE_BASED
- CONNECT_MESSAGE_BASED
- CONNECT_FULLY_SPECIFIED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fcca8da985eb669e465112886236dc96010d789
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835989"
---
# <a name="using-ioconnectinterruptex-prior-to-windows-vista"></a>Windows Vista より前の IoConnectInterruptEx の使用


Windows 2000、Windows XP、または Windows Server 2003 用のドライバーは、これらのバージョンのオペレーティングシステムで[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)を使用するために Iointex ライブラリにリンクできます。

このようなドライバーで**IoConnectInterruptEx**を使用するには、ドライバーのソースコードに Iointex .h を追加します。その直後に、Wdm または Ntddk を指定します。 Iointex .h ヘッダーは、ルーチンのプロトタイプを宣言します。 ドライバーをビルドするときは、そのドライバーが Iointex .lib に静的にリンクされていることを確認してください。

Windows Vista より前のオペレーティングシステムの場合、Iointex によって提供される**IoConnectInterruptEx**のバージョンでサポートされるのは、CONNECT\_\_指定されたバージョンのルーチンのみです。 他のバージョンが指定されている場合、ルーチンは NTSTATUS エラーコードを返し、&gt;**バージョン**-*パラメーター*を設定して、完全\_指定された\_接続します。

この動作を使用すると、ドライバーが\_ベースの接続\_使用されるように、または Windows Vista に基づく\_メッセージ\_に接続して、以前のオペレーティングシステムで指定され\_完全に\_接続するようにドライバーを作成できます。 最初に*パラメーター*-を呼び出します。&gt;**バージョン**は、\_LINE\_ベースの接続または\_メッセージ\_**ベースの接続**に相当します。 戻り値がエラーコードおよび*パラメーター*-&gt;**Version** ! = connect\_完全\_指定されている場合は、接続するために-**バージョン**に設定されている*パラメーター*を使用して操作を再試行してください&gt;10_ 完全\_指定。

次のコード例は、の手法を示しています。

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->MessageUsed is a BOOLEAN.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_MESSAGE_BASED;

// Set members of params.MessageBased here.

status = IoConnectInterruptEx(&params);

if ( NT_SUCCESS(status) ) {
    // Operation succeeded. We are running on Windows Vista.
    devExt->MessageUsed = TRUE; // We save this for posterity.
} else {
    // Check to see if we are running on an operating system prior to Windows Vista.
    if (params.Version == CONNECT_FULLY_SPECIFIED) {
        devExt->MessageUsed = FALSE;  // We're not using message-signaled interrupts.
 
        // Set members of params.FullySpecified here.
 
        status = IoConnectInterruptEx(&params);
    } else {
        // Other error.
    }
}
```

 

 




