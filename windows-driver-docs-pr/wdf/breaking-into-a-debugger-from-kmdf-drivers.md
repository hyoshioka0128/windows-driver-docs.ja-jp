---
title: KMDF ドライバーからのデバッガーへの割り込み
description: KMDF ドライバーからのデバッガーへの割り込み
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- ドライバー WDK KMDF、デバッガーの中断のデバッグ
- WDK KMDF のデバッガーの中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5afbf30ce121d9da9f2b6073cf5764dafd6ac3a
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815115"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>KMDF ドライバーからのデバッガーへの割り込み


カーネル モードのデバッガーを中断する、framework ベースのドライバーを実行する場合に、次を使用できます。

-   [ **WdfVerifierDbgBreakPoint** ](https://msdn.microsoft.com/library/windows/hardware/ff551164)場合に、関数がデバッガーを中断、 [DbgBreakOnError](registry-values-for-debugging-kmdf-drivers.md)レジストリの値を設定します。

-   [ **WDFVERIFY** ](https://msdn.microsoft.com/library/windows/hardware/ff551167)マクロは、論理式をテストし、式の評価する場合、カーネル デバッガーを中断**FALSE**場合に、 [VerifyOn](registry-values-for-debugging-kmdf-drivers.md)レジストリの値を設定します。

-   [**確認\_IS\_IRQL\_パッシブ\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff545588) IRQL では、ドライバーが実行されていない場合に、マクロがカーネル デバッガーを中断パッシブを=\_レベルと場合、 **VerifyOn**レジストリの値を設定します。

-   [ **ASSERT** ](https://msdn.microsoft.com/library/windows/hardware/ff542107)マクロは、論理式をテストし、式の評価する場合、カーネル デバッガーを中断**FALSE**します。

-   [ **ASSERTMSG** ](https://msdn.microsoft.com/library/windows/hardware/ff542113)マクロによって式をテストして、式の評価が**FALSE**、カーネル デバッガーを中断および表示可能なテキスト メッセージを表示する、デバッガー。

-   [ **DbgPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff543634)と[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)関数がデバッガーに表示可能なテキスト メッセージを指定します。

WDFVERIFY と検証用コード\_IS\_IRQL\_パッシブ\_リリースまたはデバッグ構成では、ドライバーをビルドするときに、ドライバー レベルのマクロが含まれている (無料のビルド環境と呼ばれる、またはチェック ビルド環境で Windows 7 以降)。 アサートと ASSERTMSG マクロのコードは、デバッグ構成で、ドライバーをビルドする場合にのみ、ドライバーに含まれます。

プロジェクト構成の詳細については、次を参照してください。[ドライバーをビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)します。

 

 





