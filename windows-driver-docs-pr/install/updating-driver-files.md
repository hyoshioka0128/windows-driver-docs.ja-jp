---
title: ドライバー ファイルの更新
description: ドライバー ファイルの更新
ms.assetid: e232abd9-4e51-4fa7-a00c-f5e184706222
keywords:
- ハードウェアの更新ウィザード WDK
- ドライバー ファイルの更新
- ドライバー ファイルの更新プログラム WDK
- 既存のドライバーの更新、デバイス セットアップ WDK デバイス インストール
- デバイスのインストール WDK、既存のドライバーを更新しています
- デバイス WDK、既存のドライバーの更新をインストールします。
- 既存のドライバー WDK を更新します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 571d7ad3f9fe7fa49261b5594271aadbf1ee8343
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380454"
---
# <a name="updating-driver-files"></a>ドライバー ファイルの更新





ドライバーは、次のいずれかが発生するたびに更新されます。

-   **ハードウェアの更新ウィザード**から実行している**デバイス マネージャー**します。

    **注**  以降 Windows Vista では、このウィザードの名前は、**ドライバー ソフトウェアの更新ウィザード**します。

     

-   Windows Update を実行します。

-   デバイスのインストール ソフトウェアを実行します。

-   Windows Vista 以降、行うことができます、 [PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)ツールをインストールまたは更新の管理者特権でコマンド プロンプトから、[ドライバー パッケージ](driver-packages.md)デバイス。

ソフトウェアのインストールと既存のドライバーを更新する INF ファイルを記述する場合は、次のガイドラインを使用します。

-   インストール ソフトウェアが呼び出せる[ **UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)、INF ファイルとハードウェア ID と一致するデバイス ドライバーを更新、ハードウェア ID を指定します。

    Windows Vista 以降、インストール ソフトウェア呼び出すことができますもドライバーを更新するのには、次のいずれか。

    -   [**DiInstallDriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)、事前にインストールされるドライバーとドライバーがサポートするシステムに存在するデバイスのドライバーをインストールします。
    -   [**DiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)システムに存在する指定されたデバイスのドライバー ストアから、指定したドライバーをインストールします。

    詳細については、次を参照してください。[デバイス インストール アプリケーションを記述して](writing-a-device-installation-application.md)します。

-   クラスのインストーラーと共同インストーラーする必要があります - インストールが [完了] ページへの応答をれなかったドライバーをアップグレードするときに[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-finishinstall)しない限り、絶対に必要です。 可能であれば、以前のインストールの設定から完了インストール情報を取得します。

-   クラスのインストーラーと共同インストーラーには可能なの範囲に、初期インストールを提供するまたは、既にインストールされているデバイスのドライバーを更新するかに基づいて動作避ける必要があります。

-   Windows XP では、レジストリ値で始まる**CoInstallers32**と**EnumPropPages32**の配信前に削除された[ **DIF_REGISTER_COINSTALLERS**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers). 以前のオペレーティング システム バージョンの INF ファイルか必要があります明示的にこれらの値を削除、nonappending を実行して操作を変更します。

-   Windows XP では、レジストリ値で始まる**再**と**LowerFilters**の配信前に削除された[ **DIF_INSTALLDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice). 以前のオペレーティング システム バージョンの INF ファイルか必要があります明示的にこれらの値を削除、nonappending を実行して操作を変更します。

-   *いない*使用[ **INF DelFiles ディレクティブ**](inf-delfiles-directive.md)または[ **INF RenFiles ディレクティブ**](inf-renfiles-directive.md)を更新するときドライバーです。 Windows では、特定のファイルが別のデバイスによって使用されていないことを保証できません。 (クラスのインストーラーと共同インストーラー削除したり、ファイルの名前を変更*場合*ファイルを使用しているデバイスがない確実に確認できます)。

-   使用して、 [ **INF してディレクティブ**](inf-delreg-directive.md)エントリは不要になった場合に、デバイスの以前のインストールから古いデバイスに固有のレジストリ エントリを削除します。 (グローバルのレジストリ エントリを削除しないでください)。

-   *いない*を使用して、 [ **INF DelService ディレクティブ**](inf-delservice-directive.md)で、 [ **INF DDInstall.Services セクション**](inf-ddinstall-services-section.md)に対象のコンピューターから、以前にインストールしたデバイス/ドライバーのサービスを削除します。 Windows では、特定のサービスが別のデバイスによって使用されていないことを保証できません。 (クラスのインストーラーと共同インストーラーには、サービスを削除できます*場合*サービスを使用しているデバイスがない確実に確認できます)。

-   クラスのインストーラー、共同インストーラーをクラス、またはサービスの DLL を更新する場合は、新しいバージョンに新しいファイル名を付ける必要があります。

INF ファイルの詳細については、次を参照してください。 [INF ファイルを作成する](overview-of-inf-files.md)と[INF ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)します。

 

 





