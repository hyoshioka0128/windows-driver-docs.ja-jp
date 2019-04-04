---
title: Windows 10 の新機能 Windows 用デバッグ ツール
description: Windows 10 では、Windows ツールのデバッグにはには、これらの新機能が含まれています。
ms.assetid: DCF1222F-6A67-463E-8C31-B7753CAFFC20
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5b3f05b74821862e834ed98a82adbd3b048cf403
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549238"
---
# <a name="debugging-tools-for-windows-new-for-windows-10"></a>Windows 用デバッグ ツールは:Windows 10 の新機能

## <a name="span-idwindbgpreviewspanspan-idwindbgpreviewspanspan-idwindbgpreviewspanwindbg-preview"></a><span id="Windbg_Preview"></span><span id="windbg_preview"></span><span id="WINDBG_PREVIEW"></span>Windbg のプレビュー

Windows デバッグ ツールの最新ニュースについては、[WinDbg Preview - 新](windbg-what-is-new-preview.md)を参照してください。


## <a name="span-idwindows10version1703spanspan-idwindows10version1703spanspan-idwindows10version1703spanwindows10-version-1703"></a><span id="Windows_10__version_1703"></span><span id="windows_10__version_1703"></span><span id="WINDOWS_10__VERSION_1703"></span>Windows 10 バージョン 1703

このセクションでは、Windows 10 バージョン 1703 で新しいデバッグ ツールについて説明します。

-   含む 8 つの新しい JavaScript トピック[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)
-   更新、 [ **dx (表示デバッガー オブジェクト モデルの式)** ](dx--display-visualizer-variables-.md)コマンド、コマンドの新機能が含まれます。
-   新しい[ **dtx (表示の種類 - デバッガー オブジェクト モデル情報の拡張)** ](dtx--display-type---extended-debugger-object-model-information-.md)コマンド。
-   新しい[ **! ioctldecode** ](-ioctldecode.md)コマンド。
-   更新[デバッガー エンジンのリファレンス](https://msdn.microsoft.com/library/windows/hardware/ff540540)に含める追加のインターフェイスと構造体。
-   更新[tools.ini を構成する](configuring-tools-ini.md)コマンド ライン デバッガーに対して追加のオプションをドキュメントにします。
-   75 以前ドキュメントに未記載の停止コードを発行[バグ チェック コード参照](bug-check-code-reference2.md)します。
-   新しい[イーサネット Nic を Windows 10 でのネットワーク カーネル デバッグのサポートされている](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)トピック。

## <a name="span-idwindows10version1607spanspan-idwindows10version1607spanspan-idwindows10version1607spanwindows10-version-1607"></a><span id="Windows_10__version_1607"></span><span id="windows_10__version_1607"></span><span id="WINDOWS_10__VERSION_1607"></span>Windows 10 バージョン 1607


このセクションでは、Windows 10 version 1607 で新しいデバッグ ツールについて説明します。

-   に関する新しいトピック[WinDbg を使用して UWP アプリのデバッグ](debugging-a-uwp-app-using-windbg.md)します。
-   30 のほとんどに表示した開発者のバグの更新プログラムのトピックを確認する[バグ チェック コード参照](bug-check-code-reference2.md)します。


## <a name="span-idwindows10spanspan-idwindows10spanspan-idwindows10spanwindows10"></a><span id="Windows_10"></span><span id="windows_10"></span><span id="WINDOWS_10"></span>Windows 10

-   [**(デバッグ設定の設定) の .settings** ](-settings--set-debug-settings-.md) -新しいコマンドを設定、変更、表示、読み込みおよび Debugger.Settings 名前空間の設定を保存することができます。
-   [**dx (表示 NatVis 式)** ](dx--display-visualizer-variables-.md) -新しい dx デバッガー コマンド、NatVis 拡張モデルと LINQ を使用してオブジェクト情報が表示されますサポートについて説明します。
-   デバッガーの環境で NatVis 視覚化ファイルを操作する新しいコマンド。
    -   [**.nvlist (NatVis リスト)**](-nvlist--natvis-list-.md)
    -   [**.nvload (NatVis 負荷)**](-nvload--natvis-load-.md)
    -   [**.nvunload (NatVis アンロード)**](-nvunload--natvis-unload-.md)
    -   [**.nvunloadall (NatVis は、すべてをアンロード)**](-nvunloadall--natvis-unload-all-.md)
-   [Bluetooth の拡張機能 (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)
-   [カーネル デバッガー拡張機能のストレージ](storage-kernel-debugger-extensions.md)
-   新しい Symproxy 情報を含む[SymProxy Automated Installation](symproxy-automated-installation.md)します。 さらに、次のトピックでは、新しい SymProxy 機能をカバーする更新されます。
    -   [シンボル ストアの HTTP](http-symbol-stores.md)
    -   [SymProxy](symproxy.md)
    -   [SymProxy をインストールします。](installing-symproxy.md)
    -   [レジストリを構成します。](configuring-the-registry.md)
    -   [IIS SymProxy の構成](configuring-iis-for-symproxy.md)
-   [**コマンド ライン オプションの CDB** ](cdb-command-line-options.md) - 新しいコマンド ライン オプションが追加されました。
-   [**! 分析**](-analyze.md) - UMDF 2.15 でこの拡張機能の使用に関する情報が追加されました。
-   [**! wdfkd.wdfcrashdump**](-wdfkd-wdfcrashdump.md)- UMDF 2.15 でこの拡張機能の使用に関する情報が追加されました
-   [**! irp** ](-irp.md) - 更新されました。 IRP のメジャーおよびマイナーのコードのテキストに、Windows 10 以降は、コマンドの出力に表示されます。
-   [デバッガーのマークアップ言語を使用して](debugger-markup-language-commands.md)について説明するよう更新されました - デバッガー マークアップ言語 (DML) で使用可能な動作が新しい右クリックします。
-   [クラッシュ ダンプ分析の Windows デバッガー (WinDbg) を使用して](crash-dump-files.md)-メモリ ダンプを引き継ぐ KDNET でパフォーマンスが向上しました。
-   [ユニバーサル ドライバー - ステップ バイ ステップのラボ (エコー カーネル モード) のデバッグ](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)-新しいステップ バイ ステップ ラボ WinDbg を使用して、KMDF エコー ドライバーのサンプルをデバッグする方法を示します。

 
## <a name="looking-to-download-the-debugging-tools"></a>デバッグ ツールをダウンロードしようとしていますか。

デバッグ ツールをダウンロードする方法の詳細については、[デバッグ ツールの Windows にダウンロード](debugger-download-tools.md)を参照してください。



