---
title: KMDF ドライバーからのデバッガーへの割り込み
description: KMDF ドライバーからのデバッガーへの割り込み
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- ドライバーのデバッグ WDK KMDF、デバッガーの中断
- デバッガーの中断 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dfcd119c25ef6dd25ff6fb94e62cc9159beeea0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845510"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>KMDF ドライバーからのデバッガーへの割り込み


フレームワークベースのドライバーがカーネルモードのデバッガーに割り込むようにするには、次のようにします。

-   [**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)関数は、 [dbgbreakonerror](registry-values-for-debugging-kmdf-drivers.md)値がレジストリで設定されている場合、デバッガーにブレークします。

-   [**Wdfverify**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)マクロは論理式をテストし、式が**FALSE**と評価された場合、および[verifyon](registry-values-for-debugging-kmdf-drivers.md)値がレジストリに設定されている場合、カーネルデバッガーに中断します。

-   VERIFY\_は、ドライバーが IRQL = パッシブ\_レベルで実行されていない場合、および**Verifyon**値がレジストリに設定されている場合に、カーネルデバッガーに[ **\_パッシブ\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/wdf/verify-is-irql-passive-level)のマクロが中断する\_irql です。

-   [**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))マクロは、式が**FALSE**に評価された場合に論理式をテストし、カーネルデバッガーに中断します。

-   [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)マクロは式をテストし、式が**FALSE**と評価された場合、はカーネルデバッガーを中断し、表示可能なテキストメッセージをデバッガーに提供します。

-   [**Dbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)関数と[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)関数は、表示可能なテキストメッセージをデバッガーに提供します。

WDFVERIFY と VERIFY\_のコードは、ドライバーをリリースまたはデバッグ構成 (無料のビルド環境またはチェックされたビルド環境と呼びます) でビルドするときにドライバーに含まれる\_IRQL\_パッシブ\_レベルのマクロです。Windows 7 以前)。 ASSERT マクロと ASSERTMSG マクロのコードは、デバッグ構成でドライバーをビルドする場合にのみ、ドライバーに含まれます。

プロジェクト構成の詳細については、「[ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)」を参照してください。

 

 





