---
title: KMDF ドライバーからのデバッガーへの割り込み
description: KMDF ドライバーからのデバッガーへの割り込み
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- ドライバーのデバッグ WDK KMDF、デバッガーの中断
- デバッガーの中断 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c883264ea99f46048cc65b118ebc0308210cb692
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261441"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>KMDF ドライバーからのデバッガーへの割り込み


フレームワークベースのドライバーがカーネルモードのデバッガーに割り込むようにするには、次のようにします。

-   [**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)関数は、 [dbgbreakonerror](registry-values-for-debugging-kmdf-drivers.md)値がレジストリで設定されている場合、デバッガーにブレークします。

-   [**Wdfverify**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)マクロは論理式をテストし、式が**FALSE**と評価された場合、および[verifyon](registry-values-for-debugging-kmdf-drivers.md)値がレジストリに設定されている場合、カーネルデバッガーに中断します。

-   VERIFY\_は、ドライバーが IRQL = パッシブ\_レベルで実行されていない場合、および**Verifyon**値がレジストリに設定されている場合に、カーネルデバッガーに[ **\_パッシブ\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/wdf/verify-is-irql-passive-level)のマクロが中断する\_irql です。

-   [**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))マクロは、式が**FALSE**に評価された場合に論理式をテストし、カーネルデバッガーに中断します。

-   [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)マクロは式をテストし、式が**FALSE**と評価された場合、はカーネルデバッガーを中断し、表示可能なテキストメッセージをデバッガーに提供します。

-   [**Dbgprintex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)関数と[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)関数は、表示可能なテキストメッセージをデバッガーに提供します。

WDFVERIFY と VERIFY\_のコードは\_IRQL\_パッシブ\_レベルのマクロがリリースまたはデバッグ構成でドライバーをビルドするときにドライバーに含まれています。 ASSERT マクロと ASSERTMSG マクロのコードは、デバッグ構成でドライバーをビルドする場合にのみ、ドライバーに含まれます。

プロジェクト構成の詳細については、「[ドライバーのビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)」を参照してください。

 

 





