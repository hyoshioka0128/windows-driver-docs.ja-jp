---
title: XPS フィルターの実装
description: XPS フィルターの実装
ms.assetid: 681f533f-d6f6-43a3-be0b-10d8c1a6f12e
keywords:
- XPSDrv プリンタードライバー WDK、render モジュール
- レンダーモジュール WDK XPSDrv、XPS フィルター
- XPS フィルター WDK XPSDrv
- WDK XPS をフィルター処理します
- IPrintPipelineFilter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d41f4eab5a3942abb6461e5dc65516b6cd05e82a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844840"
---
# <a name="implementing-xps-filters"></a>XPS フィルターの実装


すべての XPS フィルターは、 [Iprintpipelinefilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinefilter)インターフェイスを実装する必要があります。

[**Iprintpipelinefilter:: initializefilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)メソッドの呼び出し中に、フィルターを次のように指定する必要があります。

1.  [IPrintPipelineManagerControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinemanagercontrol)インターフェイスへのポインターをキャッシュします。

2.  [Iprintpipelinepropertybag](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinepropertybag)インターフェイスで関連データを処理します。

3.  **Iinterfiltercommunicator**インターフェイス (pIInterFilterCom) の[**Iinterfiltercommunicator:: Requestreader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iinterfiltercommunicator-requestreader)メソッドと[**Iinterfiltercommunicator:: requestreader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iinterfiltercommunicator-requestwriter)メソッドを呼び出して、プロバイダーとのコンシューマーインターフェイスを初期化します。フィルター。

データに PrintTicket セクションが含まれている場合は、Microsoft Win32 PrintTicket または PrintCapabilities API を使用してデータにアクセスできます。 XPSDrv に基づく UniDrv および PScript5 ドライバーの場合、フィルターは[Iprintcorehelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)インターフェイスコアの UniDrv または PScript5 ドライバーに構成サービスとしてアクセスできます。

フィルターは、ドライバーの設計に応じて、プロパティバッグを使用して独自の構成データにアクセスすることもできます。

フィルター間の Communicator は、フィルターパイプラインのフィルター間の通信を処理するフィルターパイプラインマネージャーの一部です。 フィルターパイプラインマネージャーによってフィルターが初期化されると、フィルター間の Communicator インターフェイス ([Iinterfiltercommunicator](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iinterfiltercommunicator)) がフィルターに渡され、フィルターに定義されている読み取りおよび書き込みインターフェイスをフィルターで取得できるようになります。

Microsoft は XPS ドキュメントおよびストリームインターフェイスを提供していますが、そのフィルターに定義されている独自のフィルター間インターフェイスを作成することもできます。 Microsoft には、次のインターフェイスが用意されています。

-   XPS のドキュメントインターフェイスは、XPS スプールファイルのさまざまな部分から読み取りおよび書き込みを行います。

-   XPS ストリームインターフェイスは、データのシリアルストリームを読み取り、書き込みます。 このインターフェイスを使用して、PDL として XPS を使用しないプリンターに、フィルターからページ記述言語 (PDL) を書き込むことができます。

フィルターは、XML Paper Specification (XPS) で定義されているレンダリングルールと PrintTicket 処理ルールに準拠している必要があります。

フィルターは、Microsoft .NET 共通言語ランタイム (CLR) または Microsoft WinFX Runtime コンポーネントに依存しないようにする必要があります。

パイプライン内のフィルターでは、ユーザーインターフェイスの内容を表示できません。

フィルターには、次の推奨事項が適用されます。

-   フィルターで個別のプロセスまたはスレッドを作成することはできません。 別のプロセスまたはスレッドが必要な場合は、フィルターがプロセスまたはスレッドの有効期間を適切に管理する必要があります。

-   フィルターには、分離された機能が必要です。 すべての機能と実装はモジュール型である必要があります。 可能な場合は、フィルター間のすべての順序と機能の依存関係を排除します。

-   フィルターは、パイプラインが順序どおりに配置されていないケースを処理する必要があります。 フィルターが予期した順序になっていない場合は、クラッシュせず、状況を適切に処理する必要があります。 フィルターが別のフィルターに依存している場合は、依存関係が指定されていない場合は、状況を適切に処理する必要があります。

フィルターに非同期通知を追加する方法の詳細については、「[印刷フィルターでの非同期通知](asynchronous-notifications-in-print-filters.md)」を参照してください。

 

 




