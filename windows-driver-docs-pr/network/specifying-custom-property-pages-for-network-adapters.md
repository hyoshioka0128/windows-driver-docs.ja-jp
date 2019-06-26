---
title: ネットワーク アダプターのカスタム プロパティ ページの指定
description: ネットワーク アダプターのカスタム プロパティ ページの指定
ms.assetid: c9d54e9b-3d11-46d1-9c24-86a802c64a7a
keywords:
- 追加レジストリ セクション WDK、ネットワークのカスタム プロパティ ページ
- カスタム プロパティ ページの WDK ネットワーク
- プロパティ ページの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6043429a91c093cc8e4b019e2196d9e0f8203124
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383637"
---
# <a name="specifying-custom-property-pages-for-network-adapters"></a>ネットワーク アダプターのカスタム プロパティ ページの指定





場合、**詳細**プロパティ ページは、Net コンポーネント (アダプター) の構成の選択内容を表示するために適していますが、1 つまたは複数のカスタム プロパティ ページを作成することができます。

**カスタム プロパティ ページを作成するには**

1.  Microsoft Win32 プロパティ ページを作成します。 プロパティ シート拡張機能を提供する DLL を作成し、 *AddPropSheetPageProc*と*ExtensionPropSheetPageProc*コールバック関数。 詳細については、Windows 2000 プラットフォーム SDK を参照してください。

2.  使用して、*追加レジストリ セクション*によって参照される、 **DDInstall**アダプターを追加するためのセクション、 **EnumPropPages32**アダプターのインスタンス キーにキー。 **EnumPropPages32**キーが 2 つの REG\_SZ 値: をエクスポートする DLL の名前、 *ExtensionPropSheetPageProc*関数との名前、 *ExtensionPropSheetPageProc*関数。 例を次に、*追加レジストリ セクション*を追加する、 **EnumPropPages32**キー。

    ```INF
    HKR, EnumPropPages32, 0, "DLL name, ExtensionPropSheetPageProc function name"
    ```

3.  アダプターの INF ファイルに含める、 **CopyFiles**プロパティ シートの拡張 DLL を Windows にコピーするセクション\\System32 ディレクトリ。 詳細については、 **CopyFiles**セクションを参照してください[INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。

4.  **DDInstall** NCF の指定、アダプターのセクション\_HAS\_UI の 1 つとして、**特性**アダプターがユーザー インターフェイスをサポートしていることを示す値。 詳細については、次を参照してください。 [DDInstall セクション](ddinstall-section-in-a-network-inf-file.md)します。

5.  プロパティ ページに変更を適用すると後、プロパティ シートの拡張 DLL が必要です。
    -   呼び出す**SetupDiGetDeviceInstallParams**
    -   設定、DI\_FLAGSEX\_PROPCHANGE\_保留中のフラグには、SP\_DEVINSTALL\_によって提供される PARAMS 構造**SetupDiGetDeviceInstallParams**
    -   最新の SP を渡す\_DEVINSTALL\_PARAMS 構造体を**SetupDiSetDeviceInstallParams**します。

        これにより、変更されたパラメーターの値を読み取ることができるように、ドライバーを再読み込みします。

 

 





