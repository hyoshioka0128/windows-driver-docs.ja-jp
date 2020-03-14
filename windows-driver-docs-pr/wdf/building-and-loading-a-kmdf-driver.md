---
title: WDF ドライバーのビルドと読み込み
description: このトピックでは、Visual Studio でドライバープロジェクトの対象となるオペレーティングシステムとフレームワークのバージョンを選択する方法について説明します。 また、共同インストーラーと、このコンポーネントをドライバーパッケージに含める必要があるかどうかを判断する方法についても説明します。
ms.assetid: 82c77b1f-4bf0-46d9-bae3-822e9be5a7fb
keywords:
- カーネルモードドライバー WDK KMDF、ドライバーのビルド
- KMDF WDK, ドライバーのビルド
- カーネルモードドライバーフレームワーク WDK、ドライバーのビルド
- カーネルモードドライバー WDK KMDF、ドライバーの読み込み
- KMDF WDK, ドライバーの読み込み
- カーネルモードドライバーフレームワーク WDK、ドライバーの読み込み
- ドライバーの構築 (WDK、KMDF)
- ドライバー WDK KMDF を読み込んでいます
- ビルドユーティリティ WDK、KMDF
- KMDF ドライバー WDK KMDF、ビルド
- KMDF ドライバー WDK KMDF、読み込み
ms.date: 05/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 73b5cb4a3e48a09a617980e4c81f23b0ef20682e
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242931"
---
# <a name="building-and-loading-a-wdf-driver"></a>WDF ドライバーのビルドと読み込み


このトピックでは、Visual Studio でドライバープロジェクトの対象となるオペレーティングシステムとフレームワークのバージョンを選択する方法について説明します。

再頒布可能フレームワークコンポーネントをドライバーパッケージに含める必要があるかどうかを判断するには、「[再頒布可能フレームワークコンポーネント](installation-components-for-kmdf-drivers.md)」を参照してください。


## <a name="which-framework-version-should-i-use"></a>どのフレームワークのバージョンを使用する必要がありますか。

*   Windows XP を対象にするには、WDF 1.9 以前を使用します。
*   Windows Vista、Windows 7、または Windows 8 を対象とするには、WDF 1.11 以前を使用します。
*   Windows 8.1 を対象にするには、KMDF 1.13 以前、または UMDF 1.x (umdf 2.0) を使用します。
*   Windows 10 バージョン1507を対象にするには、KMDF 1.15 以前、または UMDF 1.x または UMDF 2.15 以前を使用します。

KMDF と UMDF バージョンの詳細については、「 [Kmdf のバージョン履歴](kmdf-version-history.md)」と「 [umdf version history](umdf-version-history.md)」を参照してください。

* [KMDF のバージョン履歴](kmdf-version-history.md)
* [UMDF バージョン履歴](umdf-version-history.md)

## <a name="how-do-i-set-the-versions-in-visual-studio"></a>Visual Studio でバージョンを設定操作方法には


最新バージョンの Windows と最新の KMDF または UMDF バージョンのドライバープロジェクトをビルドしている場合は、既定値をそのまま使用して、この手順を省略できます。

それ以外の場合は、次の手順を実行します。

-   ソリューションを右クリックし、 **[Configuration Manager]** を選択します。  **プロジェクト構成**を目的の値 (**デバッグ**など) に設定します。
-   ドライバープロジェクトを右クリックし、 **[プロパティ]** を選択します。  **[構成プロパティ-> ドライバーの設定-> ドライバーモデル]** を開きます。  [ドライバーモデル設定](../develop/driver-model-settings-properties-for-driver-projects.md)の**Kmdf バージョン Minor (ターゲットバージョン)** 値または**UMDF version minor (ターゲットバージョン)** 値を目的の値に変更します。  **Kmdf のマイナーバージョン (最小要件)** と**UMDF バージョンマイナー (最小要件)** については、「最小要件の[指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-a-wdf-driver-for-multiple-versions-of-windows#specifying-minimum-required)」を参照してください。

Windows 10 に付属する Windows Driver Kit (WDK) を使用して、KMDF 1.9-1.29 ドライバーと、UMDF 1.9-2.29 ドライバーをビルドできます。

KMDF と UMDF バージョンの詳細については、「 [Kmdf のバージョン履歴](kmdf-version-history.md)」と「 [umdf version history](umdf-version-history.md)」を参照してください。

* [KMDF のバージョン履歴](kmdf-version-history.md)
* [UMDF バージョン履歴](umdf-version-history.md)

## <a name="linking-and-loading"></a>リンクと読み込み


Microsoft Visual Studio で Windows Driver Framework (WDF) プロジェクトをビルドすると、MSBuild によってドライバーが適切なフレームワークライブラリ、ライブラリのローダー、およびスタブファイルにリンクされます。これらはすべて WDK に含まれています。 (ライブラリとローダーも、必要に応じてドライバーパッケージと一緒に配布できるように、フレームワークの[共同インストーラー](installing-the-framework-s-co-installer.md)に含まれています)。

スタブファイルには、 **Fxdriverentry**という特殊なエントリポイントルーチンが含まれています。 MSBuild は、スタブの**Fxdriverentry**ルーチンをフレームワークベースのドライバーの最初のエントリポイントとして設定します。

オペレーティングシステムは、フレームワークベースのドライバーを読み込むときに、スタブファイルとライブラリのローダーも読み込みます。 次に、システムはスタブファイルの**Fxdriverentry**ルーチンを呼び出します。 次に、このルーチンはローダーを呼び出します。 ローダーは、ドライバーが必要とするフレームワークライブラリのバージョンを判断し、正しい[バージョンのライブラリ](framework-library-versioning.md)をカーネルモードサービスとして読み込みます (まだ読み込まれていない場合)。 最後に、ライブラリはドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンを呼び出します。

