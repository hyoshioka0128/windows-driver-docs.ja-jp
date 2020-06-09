---
title: Windows 10 用の Windows 用デバッグツール
description: Windows 10 の場合、Windows 用のデバッグツールには、これらの新機能が含まれています。
ms.assetid: DCF1222F-6A67-463E-8C31-B7753CAFFC20
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: cdcf752e3ee47a3df0eb283294e2c41b4a4f6655
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534385"
---
# <a name="debugging-tools-for-windows-new-for-windows-10"></a>Debugging Tools for Windows:Windows 10 の新機能

## <a name="span-idwindbg_previewspanspan-idwindbg_previewspanspan-idwindbg_previewspanwindbg-preview"></a><span id="Windbg_Preview"></span><span id="windbg_preview"></span><span id="WINDBG_PREVIEW"></span>Windbg プレビュー

Windows デバッグツールの最新ニュースについては、「 [WinDbg Preview-新機能](windbg-what-is-new-preview.md)」を参照してください。


## <a name="span-idwindows_10__version_1703spanspan-idwindows_10__version_1703spanspan-idwindows_10__version_1703spanwindows10-version-1703"></a><span id="Windows_10__version_1703"></span><span id="windows_10__version_1703"></span><span id="WINDOWS_10__VERSION_1703"></span>Windows 10 バージョン1703

このセクションでは、Windows 10 バージョン1703の新しいデバッグツールについて説明します。

-   [Javascript デバッガースクリプト](javascript-debugger-scripting.md)を含む8つの新しい javascript トピック
-   新しいコマンド機能を含むように、 [**dx (Display Debugger Object Model Expression)**](dx--display-visualizer-variables-.md)コマンドを更新します。
-   [新しい[**dtx (表示の種類-拡張デバッガーオブジェクトモデル情報)**](dtx--display-type---extended-debugger-object-model-information-.md) ] コマンド。
-   New [**! ioctldecode**](-ioctldecode.md)コマンド。
-   追加のインターフェイスと構造を含むように、[デバッガーエンジン参照](debugger-engine-reference.md)が更新されました。
-   コマンドラインデバッガーの追加オプションを文書化するための[ツール .ini の構成](configuring-tools-ini.md)に関する記事を更新しています。
-   発行済みの 75[バグチェックコードリファレンス](bug-check-code-reference2.md)の停止コード。
-   [Windows 10 トピックのネットワークカーネルデバッグ用の新しいイーサネット nic がサポートされて](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)います。

## <a name="span-idwindows_10__version_1607spanspan-idwindows_10__version_1607spanspan-idwindows_10__version_1607spanwindows10-version-1607"></a><span id="Windows_10__version_1607"></span><span id="windows_10__version_1607"></span><span id="WINDOWS_10__VERSION_1607"></span>Windows 10 バージョン1607


このセクションでは、Windows 10 バージョン1607の新しいデバッグツールについて説明します。

-   [WinDbg を使用した UWP アプリのデバッグ](debugging-a-uwp-app-using-windbg.md)に関する新しいトピックです。
-   「[バグチェックコードリファレンス](bug-check-code-reference2.md)」にある、最も表示の多い30個の開発者バグチェックトピックを更新します。


## <a name="span-idwindows_10spanspan-idwindows_10spanspan-idwindows_10spanwindows10"></a><span id="Windows_10"></span><span id="windows_10"></span><span id="WINDOWS_10"></span>Windows 10

-   [**. 設定 (デバッグ設定の設定)**](-settings--set-debug-settings-.md) -Debugger. settings 名前空間の設定、変更、表示、読み込み、および保存の設定を可能にする新しいコマンド。
-   [**dx (Display NatVis Expression)**](dx--display-visualizer-variables-.md) -新しい dx デバッガーコマンドについて説明します。このコマンドは、NatVis 拡張モデルと LINQ サポートを使用してオブジェクト情報を表示します。
-   デバッガー環境で NatVis ビジュアライゼーションファイルを操作する新しいコマンド。
    -   [**.nvlist (NatVis の一覧表示)**](-nvlist--natvis-list-.md)
    -   [**.nvload (NatVis の読み込み)**](-nvload--natvis-load-.md)
    -   [**.nvunload (NatVis のアンロード)**](-nvunload--natvis-unload-.md)
    -   [**.nvunloadall (NatVis のすべてアンロード)**](-nvunloadall--natvis-unload-all-.md)
-   [Bluetooth 拡張機能 (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)
-   [ストレージ カーネル デバッガー拡張機能](storage-kernel-debugger-extensions.md)
-   [Symproxy 自動インストール](symproxy-automated-installation.md)を含む新しい symproxy 情報。 さらに、次のトピックは、新しい SymProxy 機能をカバーするように更新されています。
    -   [HTTP シンボル ストア](http-symbol-stores.md)
    -   [SymProxy](symproxy.md)
    -   [SymProxy のインストール](installing-symproxy.md)
    -   [レジストリの構成](configuring-the-registry.md)
    -   [SymProxy 用の IIS の構成](configuring-iis-for-symproxy.md)
-   [**CDB のコマンドラインオプション**](cdb-command-line-options.md)-新しいコマンドラインオプションが追加されました。
-   [**! analyze**](-analyze.md) -この拡張機能を UMDF 2.15 で使用する方法に関する情報が含まれるように更新しました。
-   [**! wdfkd. wdfkd**](-wdfkd-wdfcrashdump.md)-この拡張機能を UMDF 2.15 で使用する方法に関する情報が追加されました。
-   [**! irp**](-irp.md) -更新されました。 Windows 10 以降では、コマンドの出力には、IRP のメジャーとマイナーのコードテキストが表示されます。
-   [デバッガーマークアップ言語の使用](debugger-markup-language-commands.md)-デバッガーマークアップ言語 (DML) で使用できる新しい右クリック動作を記述するように更新されました。
-   [Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)-KDNET でのメモリダンプの取得でパフォーマンスが向上しました。
-   [ユニバーサルドライバーのデバッグ-ステップバイステップラボ (Echo カーネルモード)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)-WinDbg を使用してサンプル kmdf Echo ドライバーをデバッグする方法を示す新しいステップバイステップラボラボ。

 
## <a name="looking-to-download-the-debugging-tools"></a>デバッグツールをダウンロードしていますか?

デバッグツールのダウンロードの詳細については、「 [Windows 用デバッグツールのダウンロード](debugger-download-tools.md)」を参照してください。



