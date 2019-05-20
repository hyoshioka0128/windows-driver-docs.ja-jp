---
title: 再頒布可能なフレームワーク コンポーネント
description: このトピックでは、Windows 8.1、Windows Driver Kit (WDK) の一部と、ドライバー パッケージに追加するものを確認する方法として含まれている再頒布可能フレームワークの Microsoft 提供の更新プログラムについて説明します。
ms.assetid: 63fbe66e-fa1b-4a70-a8ea-df4f3df9bad4
keywords:
- フレームワーク ベースのドライバー WDK KMDF をインストールします。
- KMDF ドライバーのインストールの INF ファイルの WDK KMDF、
- WDK KMDF ドライバーのインストール コンポーネント
ms.date: 05/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3e68121fbed77beac9066701bafc6bfb54920a56
ms.sourcegitcommit: 7bd9480d40021827e6d46f9b83638dac85380e88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875101"
---
# <a name="redistributable-framework-components"></a>再頒布可能なフレームワーク コンポーネント

このトピックでは、Windows Driver Kit (WDK) の一部と、ドライバー パッケージに追加するものを確認する方法として含まれている再頒布可能フレームワークの Microsoft 提供の更新プログラムについて説明します。

フレームワークの再頒布可能パッケージ更新プログラムを使用すれば、オペレーティング システムに含まれているよりも新しい framework バージョンで構築されたドライバーを実行できます。 たとえば、KMDF 1.11 は Windows 8 で含まれます。 Windows Vista または Windows 7 で KMDF 1.11 ドライバーを実行することができます。 これを行う前に、必ず、KMDF 1.11 framework ライブラリに以前のオペレーティング システムに含まれるフレームワーク ライブラリが置き換えられる (この場合、KMDF 1.7 と KMDF 1.9 それぞれ)。 そのためには、Microsoft 提供共同インストーラーまたは .msu ファイル、ドライバー パッケージの再配布します。

## <a name="when-do-i-need-to-include-a-co-installer-or-msu-in-my-driver-package"></a>ときに共同インストーラーまたは .msu を ドライバー パッケージに含める必要があるのでしょうか。

まず、Windows のバージョン、ドライバーは、サポートを決定します。  その指定に基づいて判断[を使用するフレームワーク バージョン](building-and-loading-a-kmdf-driver.md#which-framework-version-should-i-use)します。

選択したの WDF バージョンが、ターゲット OS に同梱されているバージョンよりも新しい場合は、ドライバー パッケージに、共同インストーラーまたは .msu ファイルを含めます。

たとえば、Windows 7 で実行するには、ドライバーをします。  WDF 1.11 または WDF 1.9 のいずれかを使用してドライバーのビルドを選択することができます。 1.9 が Windows 7 で提供される、選択した場合、システムを更新する必要はありません。 その一方で、1.11 を選択した場合は、ドライバーを WDF 1.11 更新プログラム パッケージを含める必要があります。

## <a name="should-i-include-the-co-installer-or-the-msu-file"></a>共同インストーラーまたは .msu ファイルを含める必要がありますか。

ドライバーのインストールが新しいハードウェア デバイス、システムをプラグインすることによってトリガーされるドライバーのみをインストールする場合は、ドライバー パッケージに共同インストーラーが含まれます。 」の説明に従って、INF ファイルで共同インストーラーを参照[KMDF 共同インストーラーを INF ファイルで指定する](installing-the-framework-s-co-installer.md)します。

ドライバーだけでなくアプリケーションをインストールする必要がある場合、セットアップ アプリケーションを呼び出すと、関連する MSU パッケージ (たとえば kmdf-1.11-Win.6.0.msu) 代わりに再配布する必要があります。
この場合は、INF エントリは必要ありません。

共同インストーラーと .msu ファイルの両方を必要はありません。


## <a name="where-can-i-find-these-files-and-whats-included"></a>これらのファイルを検索する場所が含まれているものとしますか?

共同インストーラーにある`%program files%\Windows Kits\<version>\redist\wdf`します。

このディレクトリには、x86 と x64 用の次のファイルが含まれています。

-   *WdfCoinstaller01007.dll*、 *WdfCoinstaller01009.dll*、 *WdfCoinstaller01011.dll* (KMDF 1.7/1.9/1.11 の共同インストーラー)。
-   *WUDFUpdate\_01007.dll*、 *WUDFUpdate\_01009.dll*、 *WUDFUpdate\_01011.dll* (共同インストーラー umdf)。
-   *winusbcoinstaller.dll*、 *winusbcoinstaller2.dll* (共同インストーラー WinUSB 1.5/1.9 用)。

MSU ファイルが希望される場合は、ダウンロードからから、形式のパッケージ (MSI) をインストールしてください[WDK 8 再頒布可能コンポーネント](https://go.microsoft.com/fwlink/p/?LinkID=253170)します。
インストール後、MSU と co-installer で確認できます`%program files%\Windows Kits\8.0\redist\wdf`します。

## <a name="co-installer-naming-and-versioning"></a>名前付け共同インストーラーとバージョン管理

共同インストーラーが名前付き**WdfCoInstaller**<em>MMmmm</em>**.dll**します。

-   *MM*メジャー バージョン番号です。
-   *mmm*マイナー バージョン番号です。

たとえば、バージョン 1.0 の共同インストーラーのファイル名は*WdfCoInstaller01000.dll*、1.11 バージョンのファイル名は*WdfCoInstaller01011.dll*します。

ドライバー パッケージに含めることが共同インストーラーのバージョンは、フレームワーク ライブラリ、ドライバーを開発するために使用のバージョンに一致する必要があります。

フレームワーク ライブラリのファイル名が、メジャー バージョン番号のみが含まれることに注意してください。 ライブラリ ファイル名の詳細については、次を参照してください。 [Framework ライブラリのバージョン管理](framework-library-versioning.md)します。
