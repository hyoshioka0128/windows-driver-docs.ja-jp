---
title: KMDF ドライバーからのデバッガーの中断
description: KMDF ドライバーからのデバッガーの中断
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- ドライバー WDK KMDF、デバッガーの中断のデバッグ
- WDK KMDF のデバッガーの中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7afbfcffa7b84d9464fbe292a193653e3597d9c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536064"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>KMDF ドライバーからのデバッガーの中断


カーネル モードのデバッガーを中断する、framework ベースのドライバーを実行する場合に、次を使用できます。

-   [ **WdfVerifierDbgBreakPoint** ](https://msdn.microsoft.com/library/windows/hardware/ff551164)場合に、関数がデバッガーを中断、 [DbgBreakOnError](registry-values-for-debugging-kmdf-drivers.md)レジストリの値を設定します。

-   [ **WDFVERIFY** ](https://msdn.microsoft.com/library/windows/hardware/ff551167)マクロは、論理式をテストし、式の評価する場合、カーネル デバッガーを中断**FALSE**場合に、 [VerifyOn](registry-values-for-debugging-kmdf-drivers.md)レジストリの値を設定します。

-   [**確認\_IS\_IRQL\_パッシブ\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff545588) IRQL では、ドライバーが実行されていない場合に、マクロがカーネル デバッガーを中断パッシブを=\_レベルと場合、 **VerifyOn**レジストリの値を設定します。

-   [ **ASSERT** ](https://msdn.microsoft.com/library/windows/hardware/ff542107)マクロは、論理式をテストし、式の評価する場合、カーネル デバッガーを中断**FALSE**します。

-   [ **ASSERTMSG** ](https://msdn.microsoft.com/library/windows/hardware/ff542113)マクロによって式をテストして、式の評価が**FALSE**、カーネル デバッガーを中断および表示可能なテキスト メッセージを表示する、デバッガー。

-   [ **DbgPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff543634)と[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)関数がデバッガーに表示可能なテキスト メッセージを指定します。

WDFVERIFY と検証用コード\_IS\_IRQL\_パッシブ\_リリースまたはデバッグ構成では、ドライバーをビルドするときに、ドライバー レベルのマクロが含まれている (無料のビルド環境と呼ばれる、またはチェック ビルド環境で Windows 7 以降)。 アサートと ASSERTMSG マクロのコードは、デバッグ構成で、ドライバーをビルドする場合にのみ、ドライバーに含まれます。

プロジェクト構成の詳細については、次を参照してください。[ドライバーをビルド](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)します。

 

 





