---
title: DirectShow のピン情報のキャッシュ
description: DirectShow のピン情報のキャッシュ
ms.assetid: 1e6a973b-32d2-4ac2-9cd6-f4d3c329cecf
keywords:
- データキャッシュの固定 WDK BDA
- WDK AVStream のキャッシュ
- DirectShow pin データキャッシュ WDK AVStream
- pin データキャッシュの WDK AVStream を更新しています
- ブロードキャストドライバーのアーキテクチャ WDK AVStream、pin データキャッシュ
- BDA WDK AVStream、ピンデータキャッシュ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e4ccb63b02c741f0a4e1d4a15ab142fb8390d6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840608"
---
# <a name="caching-pin-information-for-directshow"></a>DirectShow のピン情報のキャッシュ





アプリケーションでは、DirectShow **IFilterMapper2**インターフェイスを使用して、特定の条件を満たすフィルターを自動的に検索できます。 このアプリケーションでは、 **IFilterMapper2**から返されるフィルターの一覧を使用して、テレビ信号を受信して表示するフィルターを使用してフィルターグラフを自動的に作成できます。 指定された条件を満たすフィルターをすばやく検索するために、 **IFilterMapper2**は、以前にキャッシュに入力されたフィルターとその pin に関する情報を使用します。 次の段落の説明では、このキャッシュを*ピンデータキャッシュ*と呼びます。

Pin データキャッシュに含まれる情報には、フィルターが公開できるメディアとメディアの種類の一覧が含まれています。 **IFilterMapper2**はこのキャッシュ情報を使用して、グラフ内に既に存在するフィルターのピンに、可能なフィルターが接続できるかどうかを判断します。 この決定を行うと、フィルターのインスタンスを作成する際のオーバーヘッドが解消され、フィルターへの接続が、メディアの種類が一致しないためにフィルターに接続できないことが判断されます。 フィルターのデータキャッシュが最新ではない場合は、フィルターグラフでの接続の候補としてフィルターが誤って削除される可能性があります。

DirectShow が使用するピンデータキャッシュが最新ではないことが BDA ミニドライバーによって判断された場合、そのミニドライバーはピンデータキャッシュを更新する必要があります。これにより、ミニドライバーの BDA コンポーネントに関する BDA フィルターインスタンスの pin 情報がフィルターで正確に公開されますグラフ. BDA ミニドライバーは、次のシナリオで説明されているように、DirectShow のピンデータキャッシュを更新します。

-   ミニドライバーで、ミニドライバーがユーザーモードでの DirectShow フィルターとして BDA フィルターを提示する方法に応じて、最初に BDA フィルターインスタンスを作成するときに、BDA の pin データキャッシュを更新する必要があるかどうかは、BDA ミニドライバーです。 BDA ミニドライバーの情報 (INF) ファイルは、ミニドライバーが BDA フィルターを DirectShow フィルターとして表示するために使用するメカニズムを指定します。

    BDA ミニドライバーは通常、[カーネルストリーミング (KS) プロキシモジュール](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)(*Ksproxy.ax*) を使用して、bda フィルターを DirectShow フィルターとして表示します。 KS プロキシは、これらのフィルターのインスタンスが最初に作成されるたびに、BDA フィルターの pin 情報を公開するように、DirectShow の pin データキャッシュを自動的に更新します。 そのため、KS プロキシを使用する BDA ミニドライバーは、最初にフィルターのインスタンスを作成するときに、DirectShow の pin データキャッシュを更新するためのアクションを実行する必要はありません。 BDA フィルターが KS プロキシを介してユーザーモードに公開されている場合、フィルターの create dispatch ルーチンが返された直後に、フィルターインスタンスに存在するピンファクトリのメディアとメディアの種類がキャッシュされた情報に自動的に含まれます。

    一部の BDA ミニドライバーは、KS フィルターを DirectShow フィルターとして表示するために KS プロキシを使用しません。 たとえば、アナログテレビ信号を受信または処理するために BDA フィルターを実装する BDA レシーバーミニドライバーは、 *KSTVTune.ax*または*KSXBar.ax*モジュールのいずれかを使用して、これらの BDA フィルターを DirectShow フィルターとして表示します。 これらのモジュールは、DirectShow の pin データキャッシュを更新するために標準の KS プロキシインターフェイスメソッドを使用しないため、これらの種類の BDA フィルターの BDA ミニドライバーは、ミニドライバーがフィルターのインスタンスを最初に作成するときに、DirectShow の pin データキャッシュを更新する必要があります。 これらのフィルターのインスタンスが作成されたときに、DirectShow の pin データキャッシュが確実に更新されるように、BDA ミニドライバーは、 [**BdaFilterFactoryUpdateCacheData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdafilterfactoryupdatecachedata)関数を呼び出した直後に[**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)関数を呼び出します。フィルターの作成ディスパッチルーチンの実装。 この呼び出しでは、ミニドライバーは、フィルターのすべての初期ピンを更新するために pin 情報を渡します。

-   ピンは、フィルターの作成ディスパッチルーチンの完了後に、BDA フィルターで動的に作成できます。 最初に作成された BDA フィルターのインスタンスが、BDA フィルターのテンプレートトポロジ ([**bda\_フィルター\_テンプレート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template)) に一覧表示されているすべてのピンのインスタンスを公開していない場合、bda ミニドライバーはを呼び出す**必要があります。BdaFilterFactoryUpdateCacheData**は、フィルターのテンプレートトポロジに記載されているすべての pin に関する情報を強制的に適用します。

DirectShow の pin データキャッシュを更新しても、レジストリにタッチして変更するため、非常に大きなオーバーヘッドが発生する  **注意**してください。 さらに、DirectShow の pin データキャッシュを更新すると、DirectShow がフィルターグラフを自動的に作成するために必要な時間に影響します。 したがって、BDA ミニドライバーは、DirectShow が使用するピンデータキャッシュが最新ではないと判断した場合にのみ、可能なすべてのピンに対して**BdaFilterFactoryUpdateCacheData**を呼び出す必要があります。

 

可能な場合は、ドライバー、ファームウェア、またはハードウェアの更新が発生するたびに、BDA ミニドライバーが**BdaFilterFactoryUpdateCacheData**を呼び出す必要があります。

 

 




