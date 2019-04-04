---
title: XPS フィルターを実装します。
description: XPS フィルターを実装します。
ms.assetid: 681f533f-d6f6-43a3-be0b-10d8c1a6f12e
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- モジュール WDK XPSDrv、XPS フィルターを表示します。
- XPS は、WDK XPSDrv をフィルター処理します。
- WDK XPS をフィルター処理します。
- IPrintPipelineFilter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4b444e04e45231277c96e6798ea0bd3938e25ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558431"
---
# <a name="implementing-xps-filters"></a>XPS フィルターを実装します。


XPS のすべてのフィルターを実装する必要があります、 [IPrintPipelineFilter](https://msdn.microsoft.com/library/windows/hardware/ff554286)インターフェイス。

呼び出し中に、 [ **IPrintPipelineFilter::InitializeFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff554291)メソッドをフィルターする必要があります。

1.  キャッシュへのポインター、 [IPrintPipelineManagerControl](https://msdn.microsoft.com/library/windows/hardware/ff554303)インターフェイス。

2.  関連するデータを処理、 [IPrintPipelinePropertyBag](https://msdn.microsoft.com/library/windows/hardware/ff554320)インターフェイス。

3.  呼び出す、 [ **IInterFilterCommunicator::RequestReader** ](https://msdn.microsoft.com/library/windows/hardware/ff551054)と[ **IInterFilterCommunicator::RequestWriter** ](https://msdn.microsoft.com/library/windows/hardware/ff551057)のメソッド、**IInterfilterCommunicator**インターフェイス (pIInterFilterCom) フィルターのプロバイダーとコンシューマー インターフェイスを初期化します。

データに PrintTicket セクションが含まれている場合は、Microsoft Win32 PrintTicket または PrintCapabilities API を通じて、データをアクセスできます。 XPSDrv に基づく UniDrv と PScript5 ドライバーのフィルターにアクセスできる、 [IPrintCoreHelper](https://msdn.microsoft.com/library/windows/hardware/ff552960)構成サービスとしてのインターフェイスのコア Unidrv または PScript5 のドライバーです。

フィルターは、ドライバーの設計によって、プロパティ バッグから専用の構成データにアクセスすることもあります。

間フィルター Communicator は、フィルター パイプライン内のフィルター間の通信を処理するフィルター パイプライン マネージャーの一部です。 フィルター パイプライン マネージャーがフィルター、Communicator の間のフィルター インターフェイスを初期化します ([IInterFilterCommunicator](https://msdn.microsoft.com/library/windows/hardware/ff551050)) フィルターに渡されるため、フィルターは、読み取りを取得し、そのために定義されているインターフェイスを記述フィルターです。

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

非同期通知をフィルターに追加する方法の詳細については、[印刷フィルターで非同期通知](asynchronous-notifications-in-print-filters.md)を参照してください。

 

 




