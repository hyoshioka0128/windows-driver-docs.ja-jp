---
title: Windows Vista より前の IoConnectInterruptEx の使用
description: Windows Vista より前の IoConnectInterruptEx の使用
ms.assetid: a08b2869-93f8-440b-9fbe-068604c6007d
keywords:
- IoConnectInterruptEx
- iointex.h
- 行ベースの割り込み WDK カーネル
- メッセージ シグナル割り込み WDK カーネル
- CONNECT_LINE_BASED
- CONNECT_MESSAGE_BASED
- CONNECT_FULLY_SPECIFIED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b54195eb15989893d764b1168297de390032c099
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364942"
---
# <a name="using-ioconnectinterruptex-prior-to-windows-vista"></a>Windows Vista より前の IoConnectInterruptEx の使用


Windows 2000、Windows XP、または Windows Server 2003 用のドライバーを使用する Iointex.lib ライブラリにリンクできます[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)でこれらのバージョンのオペレーティング システム。

使用する**IoConnectInterruptEx**このようなドライバー、Wdm.h または Ntddk.h 後すぐ、ドライバーのソース コードで Iointex.h を含めます。 Iointex.h ヘッダーは、ルーチンのプロトタイプを宣言します。 ドライバーをビルドすると、Iointex.lib に静的にリンクされていることを確認します。

バージョンの Windows Vista では、以前のオペレーティング システム**IoConnectInterruptEx**接続 Iointex.lib のみをサポートによって提供される\_完全\_ルーチンのバージョンを指定します。 ルーチンが NTSTATUS エラー コードを返すし、設定、他のバージョンが指定されている場合*パラメーター*-&gt;**バージョン**connect\_完全\_指定します。

この動作を使用することができます記述には、ドライバーの接続を使用するよう\_行\_ベースまたは CONNECT\_メッセージ\_Windows Vista、および接続に基づく\_完全\_で以前に指定オペレーティング システムです。 まず**IoConnectInterruptEx**で*パラメーター*-&gt;**バージョン**接続と等しく\_行\_ベースまたは CONNECT\_メッセージ\_ベース。 戻り値がエラー コードの場合と*パラメーター*-&gt;**バージョン**! = CONNECT\_完全\_で操作を再試行して指定すると、*パラメーター*-&gt;**バージョン**接続 に設定\_完全\_に指定します。

次のコード例は、この手法を示しています。

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

 

 




