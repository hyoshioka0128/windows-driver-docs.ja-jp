---
title: WDF ドライバー (KMDF または UMDF) のテスト
description: このトピックでは、カーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) バージョン2ドライバーをテストするための推奨事項について説明します。
ms.assetid: 05545488-0114-49f5-bf8a-006a868911e8
keywords:
- カーネルモードドライバー WDK KMDF、テスト
- KMDF WDK、テストドライバー
- カーネルモードドライバーフレームワーク WDK、テストドライバー
- フレームワークベースのドライバー WDK KMDF、テスト
- ドライバーのテスト WDK、フレームワークベースのドライバー
- VerifierOn レジストリ値 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a562622f7a25e1105a0b831af5c7c7b9ee91d8d
ms.sourcegitcommit: 9a054b6012db2b6f28ac818d4656e74400945c75
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68821564"
---
# <a name="testing-a-wdf-driver-kmdf-or-umdf"></a>WDF ドライバー (KMDF または UMDF) のテスト


このトピックでは、カーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) バージョン2ドライバーをテストするための推奨事項について説明します。

ドライバーをテストするときは、次のことを行う必要があります。

-   **VerifierOn**レジストリ値を設定して、フレームワークのドライバー検証機能を有効にします。 ドライバーのデバッグとテストを行うときに使用できる**VerifierOn**およびその他のレジストリ値の詳細については、「 [Kmdf 検証の使用](using-kmdf-verifier.md)」および「 [UMDF 検証ツール](using-umdf-verifier.md)の使用」を参照してください。 フレームワークのドライバー検証機能の使用に役立つアプリケーションの詳細については、「 [WDF Verifier Control application](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)」を参照してください。

-   UMDF バージョン1と2の両方について、Wudfhost .exe で [アプリケーション検証ツール (Appverif.chm)] を有効にします。 Appverif.chm ツールは、「 [Windows 用デバッグツールのダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)」の一部としてダウンロードできます。  例:
    ```cpp
    appverif -enable handles locks heaps memory exceptions TLS -for WudfHost.exe
    ```

    これにより、フレームワークの組み込み検証が自動的に有効になります。
-   このドキュメントで説明されているドライバー検証ツールを使用します。 これらの重要なツールの詳細については、以下を参照してください。
    -   [WdfTester:WDF ドライバーテストツールセット](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdftester--wdf-driver-testing-toolset)
    -   [ドライバーの検証用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)
    -   [ドライバーのテスト用ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-testing-drivers)

ドライバーを十分にテストするには、フレームワークのドライバー検証機能とドライバー検証ツールの両方を使用する必要があります。

Microsoft Visual Studio と Windows Driver Kit (WDK) を使用したドライバーのテストに関する一般的な情報については、「[ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)と[WDF ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers/wdf/testing-a-kmdf-driver)」を参照してください。

 

 





