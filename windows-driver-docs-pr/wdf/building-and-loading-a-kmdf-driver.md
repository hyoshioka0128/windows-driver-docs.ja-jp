---
title: ビルドと WDF ドライバーの読み込み
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
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d70338ba8c3834b803fad13de109cea49061ca98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551351"
---
# <a name="building-and-loading-a-wdf-driver"></a>ビルドと WDF ドライバーの読み込み


このトピックでは、Visual Studio で、対象のオペレーティング システムとドライバーのプロジェクトのフレームワークのバージョンを選択する方法について説明します。 共同インストーラーとかどうか、ドライバー パッケージにこのコンポーネントを含める必要がありますを決定する方法についても説明します。

## <a name="which-framework-version-should-i-use"></a>フレームワーク バージョンを使用する必要がありますか。


が Windows 8.1 でのみ実行するには、ドライバーが必要な場合は、カーネル モード ドライバー フレームワーク (KMDF) バージョン 1.13 またはユーザー モード ドライバー フレームワーク (UMDF) バージョン 2.0 を使用します。

場合は、ドライバーが Windows 8.1 より前のオペレーティング システムで動作する必要があります、KMDF または UMDF version 1.11 を使用することをお勧めします。

Windows Driver Kit (WDK) に付属する Windows 8.1 をビルド KMDF 1.9、1.11 と 1.13 ドライバー、できるだけでなく、UMDF 1.9 1.11、および 2.0 のドライバーを使用することができます。

## <a name="how-do-i-set-the-versions-in-visual-studio"></a>Visual Studio のバージョンを設定する方法


最新バージョンの Windows と最新 KMDF または UMDF バージョンのドライバー プロジェクトをビルドしている場合は、既定値のままし、この手順をスキップできます。

それ以外の場合、これらの手順に従います。

-   変更、**プロジェクト構成**での設定、 **Configuration Manager**に適切な値 (など**Win7 デバッグ**)。
-   変更、KMDF\_バージョン\_わずかであるか UMDF\_バージョン\_マイナー値、[ドライバー モデルの設定](https://msdn.microsoft.com/windows-drivers/develop/driver_model_settings_properties_for_driver_projects)(11) などの適切な値にします。

KMDF および UMDF バージョンに関する詳細については、[KMDF バージョン履歴](kmdf-version-history.md)と[UMDF バージョン履歴](umdf-version-history.md)を参照してください。

## <a name="when-do-i-need-to-include-a-co-installer-or-msu-in-my-driver-package"></a>ときに共同インストーラーまたは .msu を ドライバー パッケージに含める必要があるのでしょうか。


KMDF 1.13 または UMDF 2.0 を使用して Windows 8.1 のドライバーをビルドする場合は、INF ファイルで共同インストーラー、カスタム インストーラー、または参照を含める必要はありません。

場合は、ドライバーが Windows 8.1 より前のオペレーティング システムで動作する必要があります、KMDF または UMDF version 1.11 に使用することと、ドライバー パッケージには、Microsoft 提供の framework の更新プログラムを含めることお勧めします。

Framework の更新プログラムを使用すれば、オペレーティング システムに含まれているよりも新しい framework バージョンで構築されたドライバーを実行できます。 たとえば、KMDF 1.11 は Windows 8 で含まれます。 Windows Vista または Windows 7 で KMDF 1.11 ドライバーを実行することができます。 これを行う前に、必ず、KMDF 1.11 framework ライブラリに以前のオペレーティング システムに含まれるフレームワーク ライブラリが置き換えられる (この場合、KMDF 1.7 と KMDF 1.9 それぞれ)。 そのためには、Microsoft 提供共同インストーラーまたは .msu ファイル、ドライバー パッケージの再配布します。

## <a name="linking-and-loading"></a>リンクと読み込み


適切なフレームワーク ライブラリ、ライブラリのローダー、およびスタブ ファイルは、ドライバーを Windows Driver Frameworks (WDF) MSBuild へのリンクである Microsoft Visual Studio でプロジェクトをビルドするとすべての WDK に含まれます。 (ライブラリとローダーは、framework には含まれるも[共同インストーラー](installing-the-framework-s-co-installer.md)があり、ドライバー パッケージに配布できます必要に応じて、します)。

スタブ ファイルには、特殊なエントリ ポイントのルーチンが含まれています。**FxDriverEntry**します。 MSBuild の設定、スタブの**FxDriverEntry** framework ベースのドライバーの初期のエントリ ポイントとしてルーチン。

オペレーティング システムでは、framework ベースのドライバーが読み込まれたら、スタブ ファイルとライブラリのローダーも読み込みます。 次に、システムが、スタブ ファイルを呼び出す**FxDriverEntry**ルーチン。 このルーチンは、ローダーを呼び出します。 ローダーは、ドライバーが必要ですし、適切なロード framework ライブラリのバージョンを決定します。[ライブラリのバージョン](framework-library-versioning.md)(これはまだ読み込まれていない) 場合は、カーネル モード サービスとして。 ライブラリのドライバーの呼び出す最後に、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)ルーチン。

 

 





