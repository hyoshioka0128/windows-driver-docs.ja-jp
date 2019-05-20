---
title: WDF ドライバーのビルドと読み込み
description: このトピックでは、Visual Studio で、対象のオペレーティング システムとドライバーのプロジェクトのフレームワークのバージョンを選択する方法について説明します。 共同インストーラーとかどうか、ドライバー パッケージにこのコンポーネントを含める必要がありますを決定する方法についても説明します。
ms.assetid: 82c77b1f-4bf0-46d9-bae3-822e9be5a7fb
keywords:
- カーネル モード ドライバー WDK KMDF、ドライバーの構築
- KMDF WDK、ドライバーの構築
- カーネル モード ドライバー フレームワーク WDK は、ドライバーの構築
- カーネル モード ドライバー WDK KMDF、ドライバーの読み込み
- KMDF WDK、ドライバーの読み込み
- カーネル モード ドライバー フレームワーク WDK は、ドライバーの読み込み
- ドライバー WDK、KMDF 構築
- WDK KMDF ドライバーの読み込み
- WDK、KMDF のユーティリティを構築します。
- KMDF ドライバー WDK KMDF、構築
- KMDF ドライバー WDK KMDF、読み込み
ms.date: 05/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: fcc04ad4692da02dd413c3189083b314c06f81de
ms.sourcegitcommit: 7bd9480d40021827e6d46f9b83638dac85380e88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875088"
---
# <a name="building-and-loading-a-wdf-driver"></a>WDF ドライバーのビルドと読み込み


このトピックでは、Visual Studio で、対象のオペレーティング システムとドライバーのプロジェクトのフレームワークのバージョンを選択する方法について説明します。

かどうかは、ドライバー パッケージに再頒布可能パッケージのフレームワークのコンポーネントを含める必要があります。 を確認するには、を参照してください。[再頒布可能フレームワーク コンポーネント](installation-components-for-kmdf-drivers.md)します。


## <a name="which-framework-version-should-i-use"></a>フレームワーク バージョンを使用する必要がありますか。

*   Windows XP を対象とするには、WDF 1.9 またはそれ以前を使用します。
*   Windows Vista、Windows 7、または Windows 8 を対象には、WDF 1.11 またはそれ以前を使用します。
*   Windows 8.1 をターゲットに KMDF 1.13 以前または UMDF を使用して、1.x では、または UMDF 2.0。
*   Windows 10 バージョン 1507、ターゲットに KMDF 1.15 以前または UMDF 使用 1.x では、または UMDF 2.15 またはそれ以前。

KMDF および UMDF バージョンに関する詳細については、次を参照してください。 [KMDF バージョン履歴](kmdf-version-history.md)と[UMDF バージョン履歴](umdf-version-history.md)します。

* [KMDF バージョン履歴](kmdf-version-history.md)
* [UMDF バージョン履歴](umdf-version-history.md)

## <a name="how-do-i-set-the-versions-in-visual-studio"></a>Visual Studio のバージョンを設定する方法


最新バージョンの Windows と最新 KMDF または UMDF バージョンのドライバー プロジェクトをビルドしている場合は、既定値のままし、この手順をスキップできます。

それ以外の場合、これらの手順に従います。

-   ソリューションを右クリックして**Configuration Manager**します。  設定**プロジェクト構成**に目的の値 (たとえば**デバッグ**)。
-   ドライバーのプロジェクトを右クリックして**プロパティ**します。  開いている**構成プロパティには、ドライバーが]-> [設定]、[ドライバー モデル**します。  変更、 **KMDF マイナー バージョン (ターゲットのバージョン)** または**UMDF マイナー バージョン (ターゲットのバージョン)** 値、[ドライバー モデル設定](../develop/driver-model-settings-properties-for-driver-projects.md)に目的の値。  詳細については**KMDF マイナー バージョン (最低限必要です)** と**UMDF マイナー バージョン (最低限必要です)** を参照してください[を指定する必要な最小](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-a-wdf-driver-for-multiple-versions-of-windows#specifying-minimum-required)します。

UMDF および KMDF 1.9 1.29 のドライバーをビルドする Windows 10 の 1.9 2.29 ドライバーに付属している Windows Driver Kit (WDK) を使用することができます。

KMDF および UMDF バージョンに関する詳細については、次を参照してください。 [KMDF バージョン履歴](kmdf-version-history.md)と[UMDF バージョン履歴](umdf-version-history.md)します。

* [KMDF バージョン履歴](kmdf-version-history.md)
* [UMDF バージョン履歴](umdf-version-history.md)

## <a name="linking-and-loading"></a>リンクと読み込み


適切なフレームワーク ライブラリ、ライブラリのローダー、およびスタブ ファイルは、ドライバーを Windows Driver Frameworks (WDF) MSBuild へのリンクである Microsoft Visual Studio でプロジェクトをビルドするとすべての WDK に含まれます。 (ライブラリとローダーは、framework には含まれるも[共同インストーラー](installing-the-framework-s-co-installer.md)があり、ドライバー パッケージに配布できます必要に応じて、します)。

スタブ ファイルには、特殊なエントリ ポイントのルーチンが含まれています。**FxDriverEntry**します。 MSBuild の設定、スタブの**FxDriverEntry** framework ベースのドライバーの初期のエントリ ポイントとしてルーチン。

オペレーティング システムでは、framework ベースのドライバーが読み込まれたら、スタブ ファイルとライブラリのローダーも読み込みます。 次に、システムが、スタブ ファイルを呼び出す**FxDriverEntry**ルーチン。 このルーチンは、ローダーを呼び出します。 ローダーは、ドライバーが必要ですし、適切なロード framework ライブラリのバージョンを決定します。[ライブラリのバージョン](framework-library-versioning.md)(これはまだ読み込まれていない) 場合は、カーネル モード サービスとして。 ライブラリのドライバーの呼び出す最後に、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)ルーチン。

