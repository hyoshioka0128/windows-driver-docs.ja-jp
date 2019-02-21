---
title: Understanding Tracefmt
description: Understanding Tracefmt
ms.assetid: 614be46f-8c44-43da-b4ec-7fd7195e2c08
keywords:
- Tracefmt WDK、Tracefmt について
- TMF ファイル WDK、Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d3c792dd3817124762658b1fca8c9c05c216c2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558064"
---
# <a name="understanding-tracefmt"></a>Understanding Tracefmt


## <span id="ddk_understanding_tracefmt_tools"></span><span id="DDK_UNDERSTANDING_TRACEFMT_TOOLS"></span>


[トレース プロバイダー](trace-provider.md)効率を高めるためのバイナリ形式でトレース メッセージを記録します。 読みやすい形式で、トレース メッセージを表示するには、Tracefmt 手順については、各メッセージの書式設定を適用し、メッセージが表示されますやテキスト ファイルに保存します。

> [!TIP]
> [Traceview で](traceview.md)を使用して簡単に GUI を備えた Tracefmt として同じ機能を提供します。

トレース メッセージの書式設定手順については、WPP ソフトウェア トレースを使用して、およびトレース プロバイダーが PDB シンボル ファイルのプライベートまたは完全なバージョンにし、コンパイルはトレース プロバイダーのソース コードに含まれます。 WPP プリプロセッサはプライベート シンボルから書式設定命令を抽出しで配置を[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)プロバイダー。

トレース メッセージの書式を設定するには、Tracefmt に TMF ファイルが必要です。 TMF ファイルを作成するには、Tracefmt または直接 Tracefmt TMF ファイルを行うことができます。 必須の入力を提供するのにには、次の方法のいずれかを使用します。

**Default.tmf を使用します。** ほとんどのアプリケーションとドライバーは、標準のメッセージ形式を使用するために、Default.tmf、WDK に含まれるファイルの情報を使用して、メッセージが書式設定できます。

**TMF ファイルを提供します。** 特定 TMF ファイルを指定するには、そのパスとファイル名を指定します。

**TMF ファイルのディレクトリへのパスを提供します。** Tracefmt が使用できる、 [GUID をメッセージ](message-guid.md)TMF ファイルのディレクトリ内のメッセージの書式設定命令を含む TMF ファイルを識別するためにトレース メッセージ。 メッセージの GUID は .tmf ファイル名拡張子の TMF ファイル名で構成されます。

**直接の Tracefmt TMF ファイルを作成します。** Tracefmt では、トレース プロバイダーのイメージ ファイル (.exe、.dll、または .sys) を使用して、ディレクトリ内、または内部シンボル サーバーを使用して、トレース プロバイダーのプライベート PDB シンボル ファイルを検索します。 PDB ファイル内のデータから TMF ファイルを作成し、TMF ファイルを使用して、トレース メッセージの書式を設定します。 TMF ファイルの作成時に[Tracepdb](tracepdb.md)作成、 [MOF](trace-managed-object-format--mof--file.md)コントロールの GUID と PDB ファイルで表される各トレース プロバイダーのトレース レベルが含まれています (.mof) ファイル。 MOF ファイルの名前は、トレース プロバイダーのモジュールの名前です。

トレース メッセージを書式設定後 Tracefmt がコマンドラインで、トレース メッセージを表示でき、次のファイルを作成できます。

- *出力ファイル*の書式設定済みトレース メッセージ。 トレース プロバイダーによって生成されたことの順序でメッセージが表示されます。 各メッセージには、トレースのプレフィックスが付きます。 詳しくは、次を参照してください。[トレース メッセージのプレフィックス](trace-message-prefix.md)します。

- A*概要メッセージ ファイル*のトレース メッセージが生成されたトレース セッションの情報。

イベントのトレースの詳細については、Microsoft Windows SDK のドキュメントを参照してください。 ドライバーでのイベント トレーシングの使用方法の詳細については、次を参照してください。 [WPP ソフトウェア トレース](wpp-software-tracing.md)します。
