---
title: Windows シンボル ファイルのインストール
description: Windows シンボル ファイルのインストール
ms.assetid: fbafb14c-9b92-47c5-9954-5c5ba2301c47
keywords:
- Windows のシンボル
- シンボル、ユーザー モード
ms.date: 03/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a2ec8db9b2230f4b5a2d62c0780bed6522c0f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572054"
---
# <a name="installing-windows-symbol-files"></a>Windows シンボル ファイルのインストール

Windows カーネルやドライバー、アプリケーションをデバッグする前に適切なシンボル ファイルにアクセスする必要があります。 Windows シンボルを取得する正式な方法は、Microsoft シンボル サーバーを使用します。 シンボル サーバーは必要に応じてお使いのデバッグ ツールにシンボルをダウンロードします。 シンボル ファイルがシンボル サーバーからダウンロードされると、ローカル コンピューターにキャッシュされ、アクセスが速くなります。 

1 つの簡単な使用の Microsoft シンボル サーバーに接続することができます、 [ **.symfix (シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md)コマンド。 完全な詳細については、次を参照してください。 [Microsoft パブリック シンボル](microsoft-public-symbols.md)します。

> [!IMPORTANT]
> Windows のされなくオフライン シンボル パッケージが公開されます。 高速の Windows では、Windows のデバッグ シンボルが迅速に行われた最新のリズム手段を更新します。 オンライン大幅に改善を行いました[Microsoft シンボル サーバー](microsoft-public-symbols.md)シンボルのすべての Windows バージョンと更新プログラムが利用できます。 これで、これについては見つかります[ブログ エントリ](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/)します。 
>
> インターネットに接続されていないコンピューターでシンボルを取得する方法については、[SymChk でのマニフェスト ファイルの使用に関するページ](using-a-manifest-file-with-symchk.md)をご覧ください。

ユーザー モードのアプリをデバッグする場合は、このアプリにものシンボルをインストールする必要があります。

そのシンボルがない Windows シンボルがある場合は、アプリをデバッグできます。 ただし、結果ははるかに制限されます。 アプリのコードをステップ実行することができますが、カーネル スタック トレースを取得する) などの分析が必要ですが、デバッガー アクティビティが失敗する可能性があります。
