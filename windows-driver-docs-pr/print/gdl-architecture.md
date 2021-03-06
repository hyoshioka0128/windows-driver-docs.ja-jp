---
title: GDL アーキテクチャ
description: GDL アーキテクチャ
ms.assetid: 3e796218-ab2a-40a7-a0e3-caeec5c6656e
keywords:
- GDL WDK、アーキテクチャ
- WDK GDL のスナップショットを作成します。
- スナップショット WDK GDL、スナップショットの作成
- パーサー WDK GDL、IPrintCoreHelperUni からパーサーへのアクセス
- GDL WDK、スキーマ
- GDL WDK、スナップショット
- WDK GDL のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb3467d4ddfb859c082626b34c2bc9412e1dc1d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364900"
---
# <a name="gdl-architecture"></a>GDL アーキテクチャ


このトピックでは、汎用的な記述子の言語 (GDL) のアーキテクチャについて説明します。

各 GDL データ セットを定義する必要があります、 [GDL スキーマ](gdl-schemas.md)データの形式を記述します。 データ セットが含まれる各ファイルは、GDL スキーマを参照します。 このスキーマには、データ セットがスキーマに準拠していることを確認して、スナップショットが作成されるときに、指定した変換を実行する GDL パーサーがで使用できます。 GPD で定義されているすべてのデータを Microsoft に標準のスキーマが提供されています。 さらに、パーサーには、構成可能なとしていくつかのデータを定義することができます。 その他のデータは、使用されている構成に依存するように記述できます。

仕様は、GDL スキーマに変換することができます。 データ セットが含まれる各ファイルは、GDL スキーマを参照します。 このスキーマは、データ セットがスキーマに準拠していることを確認して、スナップショットが作成されるときに、指定した変換を実行する GDL パーサーを使用できます。

データ セットと、スキーマを定義した後、クライアントは、複数のビューを作成できますか[スナップショット](gdl-snapshots.md)、さまざまな構成を指定することで、1 つのデータ セットから。 Unidrv 構成とレンダリングのプラグインは、クライアントがアクセスできる、スナップショット内のメソッドによる、 [IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)インターフェイス. GDL パーサーは、データ セットで指定されているスキーマを読み込むし、データ セットをそのスキーマに準拠していることを確認します。 データ セットが準拠していない場合、パーサーはファイルの解析にエラーを示します。

データ セットと、スキーマを定義したら、クライアントは、構成を指定することによってデータ セットのスナップショットを作成できます。

1.  プラグインへのポインターを取得、 **IPrintCoreHelperUni**インターフェイスを通じて、 [ **IPrintOemUI::PublishDriverInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)メソッド。

2.  いずれかを呼び出すことによって、スナップショットへのアクセスを要求プラグイン[ **IPrintCoreHelperUni::CreateGDLSnapshot** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperuni-creategdlsnapshot)または[ **IPrintCoreHelperUni:。CreateDefaultGDLSnapshot**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperuni-createdefaultgdlsnapshot)します。 場合、プラグイン呼び出し**CreateGDLSnapshot**、呼び出し元が、パーサーを使用して、スナップショットのビューを決定する構成を含む DEVMODE 構造体を提供します。

3.  GDL パーサーでは、データ セットをそのスキーマに準拠していることを確認します。 データ セット内で指定されているスキーマを読み込みます。 データ セットが準拠していない場合は、エラー メッセージが発行されます。

4.  GDL パーサーは GDL ソース ファイルから、内部データ構造を作成し、スキーマの指定と処理の手順については、構成に基づいて適切なビューを決定します。

5.  パーサーが XML 表現を作成します (、*スナップショット*) の処理後のデータ エントリ。 この XML スナップショットは、ストリームとしてプラグインには.

スキーマを省略した場合、パーサーはスキーマの検証を実行するだけとスナップショットの値は、スナップショットで GDL ソース ファイル内で定義された最初のバイトの文字列として表現されます。

**注**   、 **PublishDriverInterface**メソッドの一部である、 **IPrintOemUni**インターフェイスおよびその他のインターフェイスもします。 プラグインは必ずしもインターフェイスを取得できませんヘルパーからように[ **IPrintOemUI::PublishDriverInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)します。 ヘルパー インターフェイスを取得できる**IPrintOemUni::PublishDriverInterface**インターフェイスの種類によって別の場所またはプラグインの実装。

 

 

 




