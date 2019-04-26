---
title: トレース メッセージ フォーマット ファイル
description: トレース メッセージ フォーマット ファイル
ms.assetid: ac45475e-bf2d-4fa6-82fc-37ef8f4c0f6c
keywords:
- トレース メッセージのフォーマット ファイル WDK
- TMF ファイル WDK
- TMF ファイル WDK、TMF ファイルについて
- ファイルの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdb426f98efcf82bf2a409c45d55d72854729a7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354740"
---
# <a name="trace-message-format-file"></a>トレース メッセージ フォーマット ファイル


## <span id="ddk_trace_message_format_file_tools"></span><span id="DDK_TRACE_MESSAGE_FORMAT_FILE_TOOLS"></span>


*トレース メッセージ形式*(TMF) ファイルを解析するための手順を含む構造化テキスト ファイルでは、メッセージのバイナリのトレースを書式設定、[トレース プロバイダー](trace-provider.md)が生成されます。 書式設定の手順は、トレース プロバイダーのソース コードに含まれ、によって、トレース プロバイダーの PDB シンボル ファイルに追加されます、 [WPP プリプロセッサ](wpp-preprocessor.md)します。

ログに記録し、書式設定済みトレース メッセージを表示するいくつかのツールでは、TMF ファイルが必要です。 [Tracefmt](tracefmt.md)と[traceview で](traceview.md)、TMF ファイルを使用できるは、書式設定し、トレース メッセージを表示するツールを WDK または PDB シンボル ファイルから直接書式設定情報を抽出することができます。

使用して TMF ファイルを作成することができます[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt)など、 **-i** Tracefmt Tracedrv の TMF ファイルを作成するように指示するパラメーター。 詳細については、次を参照してください。[例 9。TMF ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/devtest/example-9--creating-a-tmf-file)します。

TMF ファイルがない場合、[トレース プロバイダー](trace-provider.md)を使用して、 [Tracepdb](tracepdb.md)します。 Tracepdb では、PDB シンボル ファイルの書式設定を抽出し、それらを格納する TMF ファイルを作成します。 多くのアプリケーションとドライバー開発者は、PDB シンボル ファイルではなく、TMF ファイルでは、配布を使用します。

TMF ファイルの名前は、 [GUID をメッセージ](message-guid.md)TMF ファイルに関連付けられているメッセージ。 ETW では、メッセージの GUID を使用して、特定のトレース メッセージの書式設定の指示を保持する TMF ファイルを関連付けます。

TMF ファイルには、次のデータが含まれています。

-   TMF ファイル データの抽出元となる、PDB ファイルの名前。

-   [メッセージ GUID](message-guid.md)ソース ファイルとソース ファイルの名前でトレース メッセージ。

-   トレース メッセージごとに、メッセージの種類を指定するエントリのソース コード ファイル名、行番号、メッセージの数、メッセージ定義の文字列、トレース フラグの名前、およびマクロが含まれる C 関数の名前を呼び出します。

-   トレース メッセージおよび関連付けられている内部型名で表示される値を持つ変数の一覧。 変数は、% で表される*n*メッセージ定義の文字列表記。

**注**  TMF ファイルが内部の使用のため予約されているし、形式が、Windows の異なるバージョン間で変更される可能性が。

 

 

 





