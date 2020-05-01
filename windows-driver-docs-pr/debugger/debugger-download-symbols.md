---
title: デバッグ用 Windows シンボル パッケージのダウンロード
description: このページでは、デバッグに使用される Windows シンボル パッケージをダウンロードすることができます。
keywords:
- Windows デバッグのダウンロード
- WinDbg
- ダウンロード
- 記号
- シンボルのダウンロード
ms.date: 04/26/2018
ms.localizationpriority: High
ms.openlocfilehash: cdda072873ead99d1636352092146eec94fea3fb
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007559"
---
# <a name="windows-symbol-packages"></a>Windows シンボル パッケージ

シンボル ファイルにより、コードのデバッグが簡単になります。 Windows シンボルを入手するための最も簡単な方法は、[Microsoft パブリック シンボル サーバー](microsoft-public-symbols.md)を使う方法です。 シンボル サーバーは必要に応じてお使いのデバッグ ツールにシンボルをダウンロードします。 シンボル ファイルがシンボル サーバーからダウンロードされると、ローカル コンピューターにキャッシュされ、アクセスが速くなります。 


## <a name="symbol-package-deprecation"></a>シンボル パッケージの非推奨

> [!IMPORTANT]
> Windows のオフライン シンボル パッケージの公開は終了しました。
>
> Windows の更新プログラムをリリースする頻度では、このページで提供されるパッケージで公開される Windows デバッグ シンボルはすぐに最新ではなくなります。 
> Azure ベースのシンボル ストアに移行することによって、オンラインの [Microsoft シンボル サーバー](microsoft-public-symbols.md)を大幅に改善しました。ここでは、Windows のすべてのバージョンおよび更新プログラムのシンボルを利用できます。 
> 詳細については、こちらの[ブログ記事](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/)を参照してください。 
>
> インターネットに接続されていないコンピューターでシンボルを取得する方法については、[SymChk でのマニフェスト ファイルの使用に関するページ](using-a-manifest-file-with-symchk.md)をご覧ください。

## <a name="symbol-resources-and-feedback"></a>シンボルのリソースとフィードバック

シンボルとデバッグの使用方法の詳細については、「[シンボルとシンボル ファイル](symbols-and-symbol-files.md)」を参照してください。

デバッグについてヘルプが必要な場合は、[デバッグ用のリソースに関するページ](debugging-resources.md)をご覧ください。 

シンボルに関する皆様からのフィードバックをお待ちしております。 ご意見やバグ レポートは、[windbgfb@microsoft.com](mailto:windbgfb@microsoft.com) までお送りください。 このアドレスでは技術的なサポートは提供しておりませんが、皆様からのフィードバックはシンボルの有用性について今後の改善計画を立てる際に参考にさせていただきます。 

## <a name="looking-for-related-downloads"></a>関連するダウンロードも探しますか?

- [Windows デバッグ ツールのダウンロード](debugger-download-tools.md)

- [Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

- [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロード](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

- [Windows HLK、HCK、Logo Kit のダウンロード](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)

- [Windows Insider Preview ビルドのダウンロード](https://insider.windows.com/)
