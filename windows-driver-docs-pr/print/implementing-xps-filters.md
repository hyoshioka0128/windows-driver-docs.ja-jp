---
title: XPS フィルターの実装
description: XPS フィルターの実装
ms.assetid: 681f533f-d6f6-43a3-be0b-10d8c1a6f12e
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- モジュール WDK XPSDrv、XPS フィルターを表示します。
- XPS は、WDK XPSDrv をフィルター処理します。
- WDK XPS をフィルター処理します。
- IPrintPipelineFilter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fea73b80b1c487868731a0bb4c80ea000c5ffa8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385829"
---
# <a name="implementing-xps-filters"></a>XPS フィルターの実装


XPS のすべてのフィルターを実装する必要があります、 [IPrintPipelineFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iprintpipelinefilter)インターフェイス。

呼び出し中に、 [ **IPrintPipelineFilter::InitializeFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)メソッドをフィルターする必要があります。

1.  キャッシュへのポインター、 [IPrintPipelineManagerControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iprintpipelinemanagercontrol)インターフェイス。

2.  関連するデータを処理、 [IPrintPipelinePropertyBag](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iprintpipelinepropertybag)インターフェイス。

3.  呼び出す、 [ **IInterFilterCommunicator::RequestReader** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nf-filterpipeline-iinterfiltercommunicator-requestreader)と[ **IInterFilterCommunicator::RequestWriter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nf-filterpipeline-iinterfiltercommunicator-requestwriter)のメソッド、**IInterfilterCommunicator**インターフェイス (pIInterFilterCom) フィルターのプロバイダーとコンシューマー インターフェイスを初期化します。

データに PrintTicket セクションが含まれている場合は、Microsoft Win32 PrintTicket または PrintCapabilities API を通じて、データをアクセスできます。 XPSDrv に基づく UniDrv と PScript5 ドライバーのフィルターにアクセスできる、 [IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelper)構成サービスとしてのインターフェイスのコア Unidrv または PScript5 のドライバーです。

フィルターは、ドライバーの設計によって、プロパティ バッグから専用の構成データにアクセスすることもあります。

間フィルター Communicator は、フィルター パイプライン内のフィルター間の通信を処理するフィルター パイプライン マネージャーの一部です。 フィルター パイプライン マネージャーがフィルター、Communicator の間のフィルター インターフェイスを初期化します ([IInterFilterCommunicator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/filterpipeline/nn-filterpipeline-iinterfiltercommunicator)) フィルターに渡されるため、フィルターは、読み取りを取得し、そのために定義されているインターフェイスを記述フィルターです。

Microsoft XPS ドキュメントとストリーム インターフェイスを提供するが、そのフィルターに対して定義されている独自の間のフィルター インターフェイスを作成できます。 マイクロソフトでは、次のインターフェイスを提供します。

-   XPS ドキュメントのインターフェイスは、XPS スプール ファイルの異なる部分の読み書きします。

-   XPS ストリーム インターフェイスでは、読み取り、データのシリアル ストリームを書き込みます。 PDL として XPS を使用しないプリンターにページ記述言語 (PDL) を記述するのにフィルターからこのインターフェイスを使用できます。

フィルターは、レンダリング規則とは、XML Paper Specification (XPS) で定義されている PrintTicket 処理規則に従う必要があります。

フィルターでは、Microsoft .NET 共通言語ランタイム (CLR) または Microsoft WinFX Runtime コンポーネントが依存する必要があります。

パイプライン内のフィルターでは、ユーザー インターフェイスのコンテンツが表示されない必要があります。

次の推奨事項は、フィルターに適用されます。

-   フィルターでは、個別のプロセスまたはスレッドは作成しないでください。 別のプロセスまたはスレッドが必要な場合、フィルターは正しくプロセスまたはスレッドの有効期間を管理する必要があります。

-   フィルター機能を分離する必要があります。 すべての機能と実装は、モジュール必要があります。 フィルター可能な限り間の順序と機能の依存関係を排除します。

-   フィルターをれたりするパイプラインで順不同のケースを処理する必要があります。 フィルターが想定されている順序では、クラッシュし、状況を適切に処理する必要があります。 フィルターは、別のフィルターに依存している場合、依存関係が指定されていない場合は、適切に状況を処理にする必要があります。

非同期通知をフィルターに追加する方法の詳細については、次を参照してください。[印刷フィルターで非同期通知](asynchronous-notifications-in-print-filters.md)します。

 

 




