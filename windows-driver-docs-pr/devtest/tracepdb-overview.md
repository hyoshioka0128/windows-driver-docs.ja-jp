---
title: Tracepdb の概要
description: Tracepdb の概要
ms.assetid: ec13726f-65e6-4aef-b2b1-a4bddcd73a37
keywords:
- Tracepdb WDK
- トレース メッセージの制御ファイル WDK
- TMC ファイル WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cd4d57a3e28d7f47f05d866f3ad4c5d43c661c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532575"
---
# <a name="tracepdb-overview"></a>Tracepdb の概要


[トレース プロバイダー](trace-provider.md)など、ユーザー モード アプリケーションとカーネル モード ドライバーを効率化するためのバイナリ形式で、トレース メッセージを格納します。 トレース メッセージを読み取るには、トレース プロバイダーのコード内の各トレース メッセージの指定された書式設定の指示を適用する必要があります。

[WPP プリプロセッサ](wpp-preprocessor.md)トレース プロバイダーのコードから手順については、書式設定を抽出しに追加[PDB シンボル ファイル](pdb-symbol-files.md)トレース プロバイダー。

Tracepdb がトレース プロバイダー (トレースの書式指定はパブリック シンボル ファイルから削除されます) の PDB シンボル ファイルの完全なまたはプライベートのバージョンから書式設定を抽出し、作成[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)のソース コード内の各トレース プロバイダー。 TMF ファイルは、プロバイダーのトレース メッセージの書式設定の説明のみを含むテキスト ファイルです。

読み取り可能な形式は、トレース メッセージを表示するツール[traceview で](traceview.md)と[Tracefmt](tracefmt.md)、TMF ファイルを解析し、トレース メッセージを書式設定を使用しています。 また、プライベート シンボル ファイルを配布するのではなく、ユーザーに TMF ファイルを配布することができます。

Tracepdb には、コントロールの GUID と PDB ファイルで表される各トレース プロバイダーのトレース レベルを含む MOF (.mof) ファイルが作成されます。 MOF ファイルの名前は、トレース プロバイダーのモジュールの名前です。

Tracepdb 作成こともできます、[トレース メッセージのコントロール (.tmc) ファイル](trace-message-control-file.md)を使用する場合は、ソース コード内の各トレース プロバイダーの **-c**オプション。 TMC ファイルが含まれています、[コントロール GUID](control-guid.md)と PDB ファイルで表される各トレース プロバイダーのトレース レベル。 TMC ファイルの名前はコントロールの GUID の[トレース プロバイダー](trace-provider.md)します。 Traceview でを使用する PDB ファイルがない場合は、のみ TMC ファイルについて注意する必要があります。

Tracepdb の唯一の関数では、TMF ファイルを作成します。 ただし、その他のなどのツール、 [BinPlace](binplace.md)、traceview で、や Tracefmt、その他の機能に加え、TMF ファイルを作成. 使用すると、Tracepdb を使用して、 **binplace-: tmf**コマンド、 **traceview で parsepdb**コマンド、および**tracefmt-i**コマンド。

Windows Vista より前にシステムでは、mspdb70.dll と msvcr70.dll Tracepdb が必要です。 Tracepdb.exe ファイルと同じディレクトリでこれらのファイルがない場合は、Tracepdb を使用する前に移動します。

Windows Vista より前にシステムでは、箱から Dbghelp.dll ファイルをコピーする必要があります\\&lt;*プラットフォーム*&gt; Windows Driver Kit (WDK) のサブディレクトリ (ここ&lt; *プラットフォーム*&gt;は x86、amd64、または ia64) Tracefmt.exe が配置されているディレクトリにします。

イベントのトレースの詳細については、Windows SDK のドキュメントを参照してください。 カーネル モード ドライバーとユーザー モード アプリケーションでのイベント トレーシングの使用方法の詳細については、[WPP ソフトウェア トレース](wpp-software-tracing.md)を参照してください。

 

 





