---
title: Debugging Tools for Windows のダウンロード - WinDbg
description: このページには、WinDbg などの Windows デバッグツールのダウンロードが用意されています。
keywords:
- Windows デバッグのダウンロード
- WinDbg
- ダウンロード
ms.date: 07/02/2019
ms.localizationpriority: High
ms.openlocfilehash: 9f60a3cedcae29bb2366833e77bef50d5761ca92
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007550"
---
# <a name="download-debugging-tools-for-windows"></a>Windows 用デバッグツールのダウンロード

Windows デバッガー (WinDbg) を使用して、カーネルモードとユーザーモードのコードをデバッグし、クラッシュダンプを分析して、コードの実行中に CPU レジスタを調べることができます。

## <a name="small-windbg-preview-logoimageswindbgx-preview-logopng-download-windbg-preview"></a>![小規模の windbg プレビューロゴ](images/windbgx-preview-logo.png) WinDbg Preview のダウンロード

WinDbg Preview は、最新の外観、高速なウィンドウ、本格的なスクリプトの操作性を備え、拡張可能なデバッガー データモデルを中心に構築された WinDbg の新しいバージョンです。 WinDbg プレビューは、現行の WinDbg と同じ基本エンジンを使用しているため、すべてのコマンド、拡張機能、ワークフローがこれまでどおり動作します。

 - Microsoft Store から WinDbg Preview をダウンロードします。[WinDbg プレビュー](https://www.microsoft.com/store/p/windbg/9pgjgd53tn86)。

 - インストールと構成の詳細については[、「WinDbg Preview-インストール](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)」を参照してください。

## <a name="small-classic-windbg-preview-logoimageswindbg-classic-logopng-debugging-tools-for-windows-10-windbg"></a>![小規模な従来の windbg プレビューロゴ](images/windbg-classic-logo.png) Windows 10 向けデバッグ ツール (WinDbg)

Windows 10 用のデバッグツールだけでなく、windows 10 または Visual Studio 2017 用の Windows Driver Kit (WDK) でも必要な場合は、Windows SDK からスタンドアロンコンポーネントとしてデバッグツールをインストールできます。 SDK インストールウィザードで、 **[Windows 用デバッグツール]** を選択し、他のすべてのコンポーネントの選択を解除します。

 - SDK から Windows 用デバッグツール (WinDbg) を取得します。[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。

 - [Windows 用デバッグツール (windbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/)での WinDbg とその他のデバッガーの詳細について説明します。

> [!TIP]
> Windows SDK が既にインストールされている場合は、 **[設定]** を開き、アプリ の **[& 機能]** に移動して、 **[windows ソフトウェア開発キット]** を選択し、 **[変更]** をクリックして、 **windows 用デバッグツールを追加するようにインストールを変更します。** .

-------------------

## <a name="looking-for-the-debugging-tools-for-earlier-version-of-windows"></a>以前のバージョンの Windows 用のデバッグツールをお探しですか?

以前のバージョンの Windows 用のデバッガーツールをダウンロードするには、デバッグ対象のバージョンの Windows SDK を[Windows SDK とエミュレーターのアーカイブ](https://developer.microsoft.com/windows/downloads/sdk-archive)からダウンロードする必要があります。 SDK のインストールウィザードで、 **[Windows 用デバッグツール]** を選択し、他のすべてのコンポーネントの選択を解除します。

## <a name="looking-for-related-downloads"></a>関連するダウンロードも探しますか?

 - [Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

 - [Windows デバッガーシンボル](debugger-download-symbols.md)  

 - [Windows HLK、HCK、または Logo Kit](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)

 - [Windows アセスメント & amp; デプロイメントキット (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

 - [Windows Insider Preview ビルド](https://insider.windows.com/)
