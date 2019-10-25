---
title: GDL アーキテクチャ
description: GDL アーキテクチャ
ms.assetid: 3e796218-ab2a-40a7-a0e3-caeec5c6656e
keywords:
- GDL WDK、アーキテクチャ
- スナップショットの作成 WDK GDL
- スナップショット WDK GDL、スナップショットの作成
- パーサー WDK GDL、Iprintcoreによるパーサーへのアクセス
- GDL WDK、スキーマ
- GDL WDK、スナップショット
- アーキテクチャ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef406539cb66c22840f0be4bb4660e2b66a893e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845296"
---
# <a name="gdl-architecture"></a>GDL アーキテクチャ


このトピックでは、汎用記述子言語 (GDL) のアーキテクチャについて説明します。

GDL データセットごとに、データの形式を記述する[gdl スキーマ](gdl-schemas.md)を定義する必要があります。 データセットを含む各ファイルは、GDL スキーマを参照します。 このスキーマを使用すると、GDL パーサーは、データセットがスキーマに準拠していることを確認し、スナップショットの作成時に指定された変換を実行できます。 GPD で定義されているすべてのデータについて、Microsoft は標準スキーマを提供しています。 また、パーサーを使用すると、構成可能なデータを定義できます。 その他のデータは、使用する構成によって異なる方法で記述できます。

仕様は、GDL スキーマに変換できます。 データセットを含む各ファイルは、GDL スキーマを参照します。 このスキーマを使用すると、GDL パーサーは、データセットがスキーマに準拠していることを確認し、スナップショットの作成時に指定された変換を実行できます。

データセットとスキーマが定義されると、クライアントは、異なる構成を指定することによって、1つのデータセットから複数のビュー ([スナップショット](gdl-snapshots.md)) を作成できます。 Unidrv の構成とレンダリングのプラグインの場合、クライアントは[Iprintcore/uni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)インターフェイスのメソッドを使用してスナップショットにアクセスできます。 GDL パーサーは、データセットに指定されているスキーマを読み込み、データセットがそのスキーマに準拠していることを確認します。 データセットが準拠していない場合、パーサーはファイルの解析に失敗したことを示します。

データセットとスキーマが定義された後、クライアントは構成を指定することによって、データセットのスナップショットを作成できます。

1.  このプラグインは、 [**Iprintoemui::P ublishdriverinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)メソッドを介して**Iprintcore peruni**インターフェイスへのポインターを取得します。

2.  このプラグインは、 [**IprintcoreCreateGDLSnapshot Peruni::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperuni-creategdlsnapshot)または[**Iprintcore Peruni:: CreateDefaultGDLSnapshot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperuni-createdefaultgdlsnapshot)のいずれかの呼び出しによって、スナップショットへのアクセスを要求します。 プラグインが**CreateGDLSnapshot**を呼び出すと、呼び出し元は、パーサーがスナップショットのビューを決定するために使用する構成を含む DEVMODE 構造体を提供します。

3.  GDL パーサーは、データセットに指定されているスキーマを読み込み、データセットがそのスキーマに準拠していることを確認します。 データセットが準拠していない場合は、エラーメッセージが発行されます。

4.  GDL パーサーは、GDL ソースファイルから内部データ構造を作成し、提供される構成とスキーマの処理命令に基づいて、適切なビューを決定します。

5.  パーサーは、処理されたデータエントリの XML 表現 (*スナップショット*) を作成します。 この XML スナップショットは、ストリームとしてプラグインに返されます。

スキーマを省略した場合、パーサーはスキーマの検証を実行するだけで、スナップショットの値は、GDL ソースファイルでもともと定義されていたバイトの文字列としてスナップショットに表示されます。

**Publishdriverinterface**メソッドは、 **Iprintoemuni**インターフェイスとその他のインターフェイスの一部でもある   に**注意**してください。 そのため、プラグインは必ずしも[**Iprintoemui::P ublishdriverinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)からヘルパーインターフェイスを取得するとは限りません。 このメソッドは、プラグインが実装するインターフェイスの種類に応じて、 **Iprintoemuni::P ublishdriverinterface**から、または他の場所からヘルパーインターフェイスを取得できます。

 

 

 




