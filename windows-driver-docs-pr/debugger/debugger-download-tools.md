---
title: Debugging Tools for Windows のダウンロード - WinDbg
description: このページでは、WinDbg などの Windows 向けデバッグ ツールのダウンロードを利用できます。
keywords:
- Windows デバッグのダウンロード
- WinDbg
- ダウンロード
ms.date: 05/01/2020
ms.localizationpriority: High
ms.openlocfilehash: f12bff2ee48bf0fd2912755c2a3be300b1534447
ms.sourcegitcommit: c74025e4ac60c3eb42ae80ab0d9806858527d228
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/02/2020
ms.locfileid: "82726260"
---
# <a name="download-debugging-tools-for-windows"></a>Windows 用デバッグ ツールのダウンロード

Windows デバッガー (WinDbg) を使用すると、コードの実行時にカーネル モードとユーザー モードのコードをデバッグし、クラッシュ ダンプを分析して、CPU レジスタを調べることができます。

Windows のデバッグの概要については、「[Getting Started with Windows Debugging](getting-started-with-windows-debugging.md)」(Windows のデバッグの概要) をご覧ください。

## <a name="small-windbg-preview-logo-download-windbg-preview"></a>![WinDbg Preview の小さなロゴ](images/windbgx-preview-logo.png) WinDbg Preview のダウンロード

WinDbg Preview は、最新の外観、高速なウィンドウ、本格的なスクリプトの操作性を備えた WinDbg の新しいバージョンです。 拡張可能なオブジェクト指向のデバッガー データ モデルを中心に構築されています。 WinDbg プレビューは、現行の WinDbg と同じ基本エンジンを使用しているため、すべてのコマンド、拡張機能、ワークフローがこれまでどおり動作します。

 - Microsoft Store から WinDbg Preview をダウンロードする:[WinDbg Preview](https://www.microsoft.com/store/p/windbg/9pgjgd53tn86)。

 - インストールと構成の詳細については、「[WinDbg プレビュー - インストール](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)」を参照してください。

## <a name="small-classic-windbg-preview-logo-debugging-tools-for-windows-10-windbg"></a>![以前の WinDbg Preview の小さなロゴ](images/windbg-classic-logo.png) Windows 10 向けデバッグ ツール (WinDbg)

Windows 向けデバッグ ツール (WinDbg) を SDK から入手する：[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。 Windows 用デバッグ ツールを Visual Studio の一部として使用できないため、[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) ページのダウンロード リンクを使用します。

Windows 向けのデバッグ ツールだけが必要で、Windows 10 向けの Windows Driver Kit (WDK) は不要な場合、Windows Software Development Kit (SDK) からスタンドアロン コンポーネントとしてデバッグ ツールをインストールできます。

SDK インストール ウィザードで、**Windows 向けデバッグ ツール**を選び、それ以外のすべてのコンポーネントの選択を解除します。

![デバッガーのチェック ボックスだけがオンになっている SDK ダウンロードのオプション](images/debugger-download-sdk.png)

### <a name="adding-the-debugging-tools-for-windows-if-the-sdk-is-already-installed"></a>SDK が既にインストールされている場合に、Windows 向けデバッグ ツールを追加する

Windows SDK が既にインストールされている場合、 **[設定]** を開き、 **[アプリと機能]** に移動し、 **[Windows Software Development Kit]** を選択し、 **[変更]** をクリックしてインストールを変更し、 **[Windows 向けデバッグ ツール]** を追加します。

-------------------

## <a name="looking-for-the-debugging-tools-for-earlier-versions-of-windows"></a>以前のバージョンの Windows 向けのデバッグ ツールが必要な場合

以前のバージョンの Windows 向けのデバッガー ツールをダウンロードするには、「[Windows SDK とエミュレーターのアーカイブ](https://developer.microsoft.com/windows/downloads/sdk-archive)」からデバッグするバージョン向けの Windows SDK をダウンロードする必要があります。 SDK のインストール ウィザードで、**Windows 向けデバッグ ツール**を選び、それ以外のすべてのコンポーネントの選択を解除します。

## <a name="learn-more-about-the-debuggers"></a>デバッガーについての詳細情報

WinDbg およびその他のデバッガーの詳細情報については、「[Debugging Tools for Windows (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/)」を参照してください。

## <a name="looking-for-related-downloads"></a>関連するダウンロードも探しますか?

- [Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

- [Windows シンボル パッケージ](debugger-download-symbols.md)  

- [Windows Hardware Lab Kit](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)

- [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロードとインストール](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

- [Windows Insider - Windows Preview ビルド](https://insider.windows.com/)
