---
title: コンテキスト ローカル DDI ハンドルの使用
description: コンテキスト ローカル DDI ハンドルの使用
ms.assetid: 1b3e5c29-9b9e-4c10-8fe0-706255c8fd91
keywords:
- コンテキストローカルの DDI ハンドルを使用した Direct3D バージョン 11 WDK Windows 7 の表示、遅延コンテキスト
- Direct3D バージョン 11 WDK Windows Server 2008 R2 のコンテキストローカル DDI ハンドルを使用した、遅延コンテキストの表示
- コンテキストローカルの DDI ハンドルを使用した、遅延コンテキスト WDK Windows 7 display
- コンテキストローカルの DDI ハンドルを使用した、遅延コンテキスト WDK Windows Server 2008 R2 の表示
- コンテキストローカル DDI は、WDK Windows 7 ディスプレイを処理します
- コンテキストローカル DDI は、WDK Windows Server 2008 R2 の表示を処理します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d99b842bfe045810097534aa53ae983f3b978a30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825393"
---
# <a name="using-context-local-ddi-handles"></a>コンテキスト ローカル DDI ハンドルの使用


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

各オブジェクト (たとえば、リソース、シェーダーなど) には、コンテキストローカルの DDI ハンドルがあります。

オブジェクトが3つの遅延コンテキストで使用されているとします。 このような場合、4つのハンドルは同じオブジェクト (遅延コンテキストごとに1つのハンドルと、イミディエイトコンテキストの別のハンドル) を参照します。 各コンテキストはスレッドによって同時に操作できるため、コンテキストローカルハンドルを使用すると、複数の CPU スレッドが同様のメモリ (意図的または意図せずに) に対して競合を防ぐことができます。 コンテキストローカルハンドルは、コンテキストごとに論理的に関連付けられているこのデータの大部分をドライバーが変更する必要があるため、直感的にもわかります (たとえば、オブジェクトがコンテキストによってバインドされている場合など)。

それでも、直接コンテキストハンドルと遅延コンテキストハンドルは区別されています。 特に、直前のコンテキストハンドルは、割り当てられた最初のハンドルと破棄された最後のハンドルであることが保証されます。 対応するイミディエイトコンテキストハンドルは、各遅延コンテキストハンドルの "オープン" 中に提供され、それらをリンクします。 現在、デバイスごとの DDI ハンドルを持つオブジェクトの概念はありません (つまり、直前のコンテキストハンドルの後に作成されるハンドルであり、コンテキストハンドルの作成によって順番に参照されるだけです)。

一部のハンドルは、他のハンドルと依存関係があります (たとえば、ビューは対応するリソースに依存しています)。 直前のコンテキストに存在する作成と破棄の順序付けの保証は、遅延コンテキストハンドルにも拡張されます (つまり、ランタイムはコンテキストローカルのビューハンドルを作成する前にコンテキストローカルのリソースハンドルを作成します)。リソースとランタイムは、ランタイムがコンテキストローカルのビューハンドルをすべて破棄した後に、コンテキストローカルのリソースハンドルを破棄します。 ランタイムは、コンテキストローカルハンドルを作成するときに、対応するコンテキストローカルの依存関係ハンドルも提供します。

### <a name="span-iddriver_data_organizationspanspan-iddriver_data_organizationspandriver-data-organization"></a><span id="driver_data_organization"></span><span id="DRIVER_DATA_ORGANIZATION"></span>ドライバーデータの編成

注意が必要なドライバーデータ組織に関しては、いくつかの懸念事項があります。 Direct3D バージョン10と同様に、データの適切な局所性により、API とドライバーの間のキャッシュミスを減らすことができます。 また、データの適切な局所性によってキャッシュスラッシングが妨げられることもあります。これは、頻繁にアクセスされるデータの複数の部分がすべて同じキャッシュインデックスに解決され、キャッシュの関連を使い果たすと発生します。 この DDI は、Direct3D バージョン10以降、ドライバーがハンドルを満たすために必要なメモリの量と、ハンドルの値を割り当てる API を API に通知するために、ドライバーによって manifesting されることを防ぐために設計されています。 ただし、新しいスレッドに関連する懸念は、Direct3D バージョン11のタイムフレームの DDI 設計に影響します。

通常、コンテキストローカルハンドルは、コンテキストごとにオブジェクトデータを関連付ける方法を提供します。これにより、スレッド間の競合の問題が回避されます。 ただし、このようなデータは遅延コンテキストごとにレプリケートされるため、このようなデータのサイズは大きな問題になります。 これにより、直接のコンテキストハンドルと遅延コンテキストハンドルの間で読み取り専用データを共有する自然な合理化が提供されます。 遅延コンテキストハンドルの作成時には、ハンドル間の接続を確立するためのコンテキストハンドルが直接提供されます。 ただし、遅延コンテキストの外部にあるすべてのデータは、API データの局所性を向上させます。また、読み取り専用データに間接的に間接的なレベルを追加することで、局所性の利点が読み取り専用データに拡張されるのを防ぐことができます。 一部の読み取り専用データは、局所性がデータの重複を正当化する場合、各コンテキストハンドル領域にレプリケートできます。 ただし、遅延されたコンテキストハンドルをすべてバックアップするメモリは、そのデータが比較的大きく、他のデータほど頻繁にアクセスされない場合に、ハンドルとは別のデータを再配置することができるという premium で考慮する必要があります。 遅延したコンテキストハンドルに関連付けられているデータの種類はすべて、高頻度のデータであることが理想的です。そのため、データは再配置を検討するのに十分な大きさではありません。 当然ながら、ドライバーは競合している動機のバランスを取る必要があります。

ドライバーデータのデザインを Direct3D version 10 と効率的に互換性を持たせるために、異なるの実装ではありませんが、読み取り専用データは、即時コンテキストがデータを処理するように連続して配置する必要があります (ただし、それ以降は分離されています)。 ドライバーがこの設計を使用する場合、ドライバーは、直接のコンテキストハンドルデータと読み取り専用データの間にキャッシュ行の埋め込みが必要であることを認識している必要があります。 スレッドでは、各コンテキストが頻繁にデータを処理する可能性があるため (同時に実行されない場合)、即時コンテキストハンドルデータと遅延コンテキストハンドルデータの間で、キャッシュラインの埋め込みが使用されていない場合、偽共有の遅延が発生します。 ドライバーの設計は、ポインターが確立され、コンテキストハンドルのメモリ領域間で定期的に走査される場合に、マニフェストを cognizant にする必要があります。

Direct3D ランタイムは、遅延コンテキストローカルハンドルに対して、次の Direct3D 11 DDI を使用します。

-   [**CheckDeferredContextHandleSizes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_checkdeferredcontexthandlesizes)関数は、遅延コンテキストハンドルのハンドルデータを保持するドライバープライベートメモリ空間のサイズを確認します。

-   [**CalcDeferredContextHandleSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)関数は、遅延コンテキストのメモリ領域のサイズを決定します。

Direct3D ランタイムで、ドライバーが必要とする遅延コンテキストハンドルサイズを取得するには、上記の DDI 関数を使用する必要があります。 イミディエイトコンテキストのオブジェクトを作成した直後に、ランタイムは[**CalcDeferredContextHandleSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcdeferredcontexthandlesize)を呼び出して、ドライバーがこのオブジェクトへの遅延コンテキストハンドルを満たすために必要なストレージ領域の量をドライバーに照会します。 ただし、Direct3D API は、アクセスする一意のハンドルサイズと値の数を決定することによって、CLS メモリアロケーターを調整する必要があります。ランタイムは、ドライバーの[**CheckDeferredContextHandleSizes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_checkdeferredcontexthandlesizes)関数を呼び出してこの情報を取得します。 そのため、デバイスのインスタンス化中に、API は、遅延コンテキストハンドルサイズの配列をダブルポーリングで要求します。 最初のポーリングは、返されるサイズの数を要求し、2番目のポーリングが配列に渡され、各サイズの値を取得します。 ドライバーは、ハンドルとハンドルの種類を満たすために必要なメモリの量を示す必要があります。 ドライバーは、特定のハンドルの種類に関連付けられている複数のサイズを返すことができます。 ただし、ドライバーが**CalcDeferredContextHandleSize**から値を返すことはありません。これは、 **CheckDeferredContextHandleSizes**配列では返されませんでした。

DDI ハンドルを作成するために、遅延コンテキストの create メソッドが使用されます。 たとえば、 [**createblendstate (D3D10\_1)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_1ddi_createblendstate)と[**destroyblendstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyblendstate)関数を調べます。 HDEVICE は、自然なコンテキストではなく、適切な遅延コンテキストを指します。その他の CONST 構造体ポインターは**NULL**です (オブジェクトに依存関係がないと仮定します)。また、D3D10DDI\_HRT\* ハンドルは、対応するイミディエイトコンテキストオブジェクトに対する D3D10DDI\_H\* ハンドルです。

依存関係を持つオブジェクト (たとえば、ビューが対応するリソースに依存関係を持つ場合) では、依存関係ハンドルを提供する構造体のポインターが**NULL**ではありません。 ただし、構造体の有効なメンバーは依存関係ハンドルだけです。一方、残りのメンバーはゼロで埋められます。 例として、ランタイムが遅延コンテキストでこの関数を呼び出すと、ドライバーの[**CREATESHADERRESOURCEVIEW (D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createshaderresourceview)関数への呼び出しの[**D3D11DDIARG\_CREATESHADERRESOURCEVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createshaderresourceview)ポインターは**NULL**になりません。 この CreateShaderResourceView (D3D11) 呼び出しでは、ランタイムは、リソースの適切なコンテキストローカルハンドルを D3D11DDIARG\_CREATESHADERRESOURCEVIEW の**hDrvResource**メンバーに割り当てます。 ただし、D3D11DDIARG\_CREATESHADERRESOURCEVIEW の残りのメンバーはゼロで埋められます。

次のコード例は、Direct3D ランタイムがアプリケーションの作成要求を変換する方法と、遅延コンテキストを最初に使用してユーザーモードの表示ドライバーを呼び出し、即時および遅延コンテキストを作成する方法を示しています。 アプリケーションが**ID3D11Device:: CreateTexture2D**を呼び出すと、次の "リソース作成" セクションのランタイムコードが開始されます。 アプリケーションが**ID3D11Device:: CopyResource**を呼び出すと、次の "遅延コンテキストリソースの使用" セクションのランタイムコードが開始されます。

```cpp
// Device Create
 IC::pfnCheckDeferredContextHandleSizes( hIC, &u, NULL );
pArray = malloc( u * ... );
IC::pfnCheckDeferredContextHandleSizes( hIC, &u, pArray );

// Resource Create
 s = IC::pfnCalcPrivateResourceSize( hIC, &Args );
pICRHandle = malloc( s );
 IC::pfnCreateResource( hIC, &Args, pICRHandle, hRTResource );
 s2 = IC::pfnCalcDeferredContextHandleSize( hIC, D3D10DDI_HT_RESOURCE, pICRHandle );

// Deferred Context Resource Usage
pDCRHandle = malloc( s2 );
 DC::pfnCreateResource( hDC, NULL, pDCRHandle, pICRHandle );
```

### <a name="span-idissues_with_pfnseterrorcbspanspan-idissues_with_pfnseterrorcbspanissues-with-pfnseterrorcb"></a><span id="issues_with_pfnseterrorcb"></span><span id="ISSUES_WITH_PFNSETERRORCB"></span>PfnSetErrorCb に関する問題

どの create 関数もエラーコードを返しません。これは、Direct3D バージョン11スレッドモデルに最適であると考えられます。 すべての create 関数は、 [**pfnSetErrorCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)を使用してドライバーからエラーコードを取得します。 Direct3D バージョン10ドライバーモデルとの互換性を最大限に高めるために、エラーコードを返す新しい DDI 作成関数は導入されていませんでした。 その代わりに、ドライバーは、作成関数の間に**pfnSetErrorCb**と共に、統合されたデバイス/即時コンテキスト D3D10DDI\_HRTCORELAYER handle を使用し続ける必要があります。 ドライバーがコマンドリストをサポートする場合、ドライバーは、対応するコンテキストに関連付けられている適切な**pfnSetErrorCb**を使用する必要があります。 つまり、遅延コンテキストエラーは、対応するハンドルを使用して、 **pfnSetErrorCb**に対する遅延コンテキストの特定の呼び出しに進む必要があります。

遅延コンテキストでは、前に D3DDDIERR\_DEVICEREMOVED ( [**Draw**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_draw)、 [**setblendstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setblendstate)など) のみを許可していた DDI[**関数から、OUTOFMEMORY の呼び出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)を使用して E\_を返すことができます。永続的のメモリ需要は、DDI 関数の呼び出しごとに増加します。 Direct3D API はローカルコンテキストの削除をトリガーし、このような障害が発生した場合にドライバーを支援します。これにより、部分的に構築されたコマンド一覧が効果的によっされます。 アプリケーションは、コマンドリストを記録していると判断し続けます。ただし、アプリケーションが最終的に**Finish commandlist**関数を呼び出すと、 **commandlist コマンド**は、OUTOFMEMORY\_のエラーコードを返します。

 

 





