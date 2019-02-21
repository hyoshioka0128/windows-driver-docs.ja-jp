---
title: 再頒布可能フレームワーク コンポーネント
description: このトピックでは、Windows 8.1、Windows Driver Kit (WDK) の一部と、ドライバー パッケージに追加するものを確認する方法として含まれている再頒布可能フレームワークの Microsoft 提供の更新プログラムについて説明します。
ms.assetid: 63fbe66e-fa1b-4a70-a8ea-df4f3df9bad4
keywords:
- フレームワーク ベースのドライバー WDK KMDF をインストールします。
- KMDF ドライバーのインストールの INF ファイルの WDK KMDF、
- WDK KMDF ドライバーのインストール コンポーネント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73a7404106beb9881c7764c25c3fe4f24bc782be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553862"
---
# <a name="redistributable-framework-components"></a>再頒布可能フレームワーク コンポーネント


このトピックでは、Windows 8.1、Windows Driver Kit (WDK) の一部と、ドライバー パッケージに追加するものを確認する方法として含まれている再頒布可能フレームワークの Microsoft 提供の更新プログラムについて説明します。

かどうかは、すべてのドライバー パッケージに、framework の更新プログラムを含める必要があります。 を確認するには、を参照してください。 [WDF ドライバーの読み込みのビルドと](building-and-loading-a-kmdf-driver.md)します。 ない場合は、このトピックをスキップします。

## <a name="should-i-include-the-co-installer-or-the-msu-file"></a>共同インストーラーまたは .msu ファイルを含める必要がありますか。


ドライバーのインストールが新しいハードウェア デバイス、システムをプラグインすることによってトリガーされるドライバーのみをインストールする場合は、ドライバー パッケージに共同インストーラーが含まれます。 」の説明に従って、INF ファイルで共同インストーラーを参照[KMDF 共同インストーラーを INF ファイルで指定する](installing-the-framework-s-co-installer.md)します。

ドライバーだけでなくアプリケーションをインストールする必要がある場合、セットアップ アプリケーションを呼び出すと、関連する MSU パッケージ (たとえば kmdf-1.11-Win.6.0.msu) 代わりに再配布する必要があります。 Src、WDK でこのようなアプリケーションのサンプルが見つかります\\全般\\installwdf ディレクトリ。

後者の場合、INF エントリは必要ありません。

## <a name="where-can-i-find-these-files-and-whats-included"></a>これらのファイルを検索する場所が含まれているものとしますか?


Visual Studio で、ドライバーをビルドすると、MSBuild は、ドライバーのと共に、結果として得られるパッケージ ディレクトリに共同インストーラーを配置します。*sys*と INF ファイル。

再頒布可能パッケージのフレームワークの更新プログラム ファイルの完全なセットにある *%programfiles%*\\windows キット\\*&lt;WDK バージョン&gt;* \\redist\\wdf します。

このディレクトリには、x86 と x64 用の次のファイルが含まれています。

-   *WdfCoinstaller01009.dll*、 *wdfcoinstaller01011.dll* (共同インストーラー KMDF 1.9/1.11 用)。
-   *WUDFUpdate\_01009.dll*、 *WUDFUpdate\_01011.dll* (共同インストーラー umdf)。
-   *winusbcoinstaller.dll*、 *winusbcoinstaller2.dll* (共同インストーラー WinUSB 1.5/1.9 用)。
-   *WinUSB\_1.9.msu* – WinUSB バージョン 1.9 の更新プログラム、としても使用可能[KB971286](http://support.microsoft.com/kb/971286)します。
-   *kmdf 1.11 Win 6.0.msu*、 *kmdf 1.11 Win 6.1.msu* -KMDF 1.11 Windows Vista (v6.0) の Windows 更新プログラム パッケージ/Windows 7 (バージョン 6.1)。
-   *umdf 1.11 Win 6.0.msu*、 *umdf 1.11 Win 6.1.msu* – UMDF 1.11 Windows Vista (v6.0) の Windows 更新プログラム パッケージ/Windows 7 (バージョン 6.1)。

## <a name="co-installer-naming-and-versioning"></a>名前付け共同インストーラーとバージョン管理


共同インストーラーが名前付き**WdfCoInstaller**<em>MMmmm</em>**.dll**します。

-   *MM*メジャー バージョン番号です。
-   *mmm*マイナー バージョン番号です。

たとえば、バージョン 1.0 の共同インストーラーのファイル名は*WdfCoInstaller01000.dll*、1.11 バージョンのファイル名は*WdfCoInstaller01011.dll*します。

ドライバー パッケージに含めることが共同インストーラーのバージョンは、フレームワーク ライブラリ、ドライバーを開発するために使用のバージョンに一致する必要があります。

フレームワーク ライブラリのファイル名が、メジャー バージョン番号のみが含まれることに注意してください。 ライブラリ ファイル名の詳細については、次を参照してください。 [Framework ライブラリのバージョン管理](framework-library-versioning.md)します。

 

 





