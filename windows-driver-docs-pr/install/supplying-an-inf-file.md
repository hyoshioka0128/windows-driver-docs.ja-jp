---
title: INF ファイルの提供
description: INF ファイルの提供
ms.assetid: 208726d9-6f62-46a4-84a1-6fab3895bbe3
keywords:
- ドライバーパッケージ WDK、INF ファイル
- WDK、INF ファイルをパッケージ化する
- INF ファイル WDK, INF ファイルについて
- 情報ファイル WDK
- .inf ファイル
- デバイスのインストール WDK、INF ファイル
- デバイスのインストール WDK, INF ファイル
- デバイスのインストール WDK、INF ファイル
- INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a7f33c3a70b7f75847ab02a0031d5bd123c26c7
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862975"
---
# <a name="supplying-an-inf-file"></a>INF ファイルの提供





すべてのドライバーパッケージには、デバイスをインストールするときに[デバイスのインストールコンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))が読み取る INF ファイルが含まれている必要があります。 INF ファイルはインストールスクリプトではありません。 これは、ドライバーファイル、レジストリエントリ、デバイス Id、[カタログファイル](catalog-files.md)、およびデバイスまたはドライバーのインストールに必要なバージョン情報を含む、デバイスとドライバーの情報を提供する、ASCII または Unicode のテキストファイルです。 INF は、デバイスまたはドライバーが最初にインストールされたときだけでなく、ユーザーがデバイスマネージャーによってドライバーの更新を要求したときにも使用されます。

INF ファイルの正確な内容と形式は、デバイスの[セットアップクラス](device-setup-classes.md)によって異なります。 [Inf セクションの概要](summary-of-inf-sections.md)各種類の inf で必要な情報について説明します。 一般に、製造元ごとの情報は[ **「INF*モデル*」セクション**](inf-models-section.md)にあります。 「**モデル**」セクションのエントリは、モデル固有の詳細が含まれている「 [**INF *ddinstall* 」セクション**](inf-ddinstall-section.md)を参照してください。

Microsoft Windows Driver Kit (WDK) の *\\tools*ディレクトリに用意されている[InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)ツールを使用すると、すべてのクロスクラスの INF セクションとディレクティブの構文と構造、およびプリンターを除くすべてのセットアップクラスのクラス固有の拡張機能を確認できます。

Windows 2000 以降では、すべてのバージョンの Windows オペレーティングシステムにインストールするために1つの INF ファイルを使用できます。 詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。 デバイスが国際市場で販売される場合は、[国際対応の INF ファイルを作成](creating-international-inf-files.md)する必要があります。 関連するローカリティによっては、国際 INF ファイルが ASCII ではなく Unicode ファイルであることが必要になる場合があります。

ドライバーの INF ファイルを作成するには、WDK が提供するサンプルのいずれかを変更することをお勧めします。 ほとんどの WDK サンプルドライバーには、サンプルドライバーと同じディレクトリにある INF ファイルが含まれています。

INF ファイルの詳細については、「 [Inf ファイルの作成](overview-of-inf-files.md)」、「 [InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)のドキュメント」、「WDK のデバイス固有のドキュメント」、および「デバイス用のサンプルドライバー」で提供されている inf ファイルを参照してください。

 

 





