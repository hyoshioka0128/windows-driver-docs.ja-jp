---
title: コンテキスト ローカル DDI ハンドルの使用
description: コンテキスト ローカル DDI ハンドルの使用
ms.assetid: 1b3e5c29-9b9e-4c10-8fe0-706255c8fd91
keywords:
- Direct3D のバージョン 11 WDK Windows 7 を表示するコンテキスト ローカル DDI ハンドルを使用して、コンテキストの遅延
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 表示、コンテキストのローカル DDI ハンドルを使用して、遅延のコンテキスト
- ローカル コンテキスト DDI ハンドルを使用して遅延コンテキスト WDK Windows 7 で表示します。
- 遅延コンテキスト WDK Windows Server 2008 R2 を表示するコンテキスト ローカル DDI ハンドルを使用します。
- ローカル コンテキスト DDI WDK Windows 7 の表示を処理します。
- ローカル コンテキスト DDI WDK Windows Server 2008 R2 の表示を処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eba46348708bb01572e3f9aa2a0b153052d622d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570279"
---
# <a name="using-context-local-ddi-handles"></a>コンテキスト ローカル DDI ハンドルの使用


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

(たとえば、およびリソース、シェーダー、)、各オブジェクトには、ローカル コンテキスト DDI ハンドルがあります。

たとえば、遅延の 3 つのコンテキストでオブジェクトを使用します。 このような状況では、4 つのハンドルを (遅延コンテキストごとに 1 つのハンドル) とイミディ エイト コンテキストの別のハンドルに同じオブジェクトを参照してください。 各コンテキストは、スレッドが同時に操作できる、ために、ローカル コンテキスト ハンドルは、複数の CPU スレッド競合しませんのようなメモリを (意図的にまたは誤って) を確認します。 ローカル コンテキスト ハンドルは、ドライバーおそらく必要があります変更ためこのままでコンテキストごとに論理的に関連付けられているデータの多くにも直観的な (たとえば、オブジェクト可能性があります、コンテキストによってバインドや)。

遅延コンテキスト ハンドルとイミディ エイト コンテキスト ハンドルの区別があります。 具体的には、最初に割り当てられているハンドルが破棄される最後のハンドルをされるようにするため、イミディ エイト コンテキスト ハンドルが保証されます。 対応するイミディ エイト コンテキスト ハンドルは、それらをリンクするには、各遅延コンテキスト ハンドルの「開く」の中に提供されます。 現在、デバイスごとの DDI ハンドルを持つオブジェクトの概念はありません (前に作成され、イミディ エイト コンテキスト ハンドルの後に破棄されるハンドルは、し、コンテキスト ハンドルの作成での順序でのみ参照されます)。

ハンドルをいくつか他のハンドルとの依存関係がある (たとえば、ビュー、依存関係がある、対応するリソース)。 作成と破棄の順序の保証に拡張は、イミディ エイト コンテキストに存在する遅延コンテキスト ハンドルも (は、ランタイム コンテキストのローカル リソース ハンドルを作成、実行時にすべてのコンテキストのローカル ビュー ハンドルを作成する前にリソース、およびランタイム ハンドルを破棄するコンテキストのローカル リソース、ランタイムは、そのリソースへのすべてのコンテキストのローカル ビュー ハンドルを破棄した後)。 ランタイムは、ローカル コンテキストのハンドルを作成するとき、ランタイムは、対応するコンテキストのローカルの依存関係ハンドルもを提供します。

### <a name="span-iddriverdataorganizationspanspan-iddriverdataorganizationspandriver-data-organization"></a><span id="driver_data_organization"></span><span id="DRIVER_DATA_ORGANIZATION"></span>ドライバーのデータの編成

これには注意が必要なドライバーのデータ組織に関するいくつかの問題があります。 Direct3D のバージョン 10 のようなデータの適切な局所性は、API とドライバーの間のキャッシュ ミス数を減らすことができます。 データの適切な局所性が同じキャッシュのインデックスと消費データに複数のアクセス頻度の高いデータすべてを解決するときに発生するキャッシュ スラッシングを防ぐことができますも、キャッシュの連想します。 DDI は、通知、API、ドライバーによってドライバーでのハンドルと、ハンドルの値を割り当てる API を満たすために必要なメモリの量を示してから、このような問題を回避する Direct3D のバージョン 10 以降設計されています。 ただし、新しいスレッドに関連する問題、Direct3D のバージョン 11 タイム フレームで DDI 設計に影響します。

当然ながら、ローカル コンテキスト ハンドルは、オブジェクトごとに、データ コンテキストのスレッド間で競合の問題を回避できますを関連付けるための手段を提供します。 ただし、遅延コンテキストごとに、このようなデータをレプリケートするため、このようなデータのサイズには、主な懸念です。 イミディ エイト コンテキスト ハンドルと遅延のコンテキスト ハンドルの間の読み取り専用のデータを共有する自然の合理化を提供します。 遅延コンテキスト ハンドルの作成時に、イミディ エイト コンテキスト ハンドルがハンドルの間の接続を確立するために提供されます。 ただし、遅延コンテキスト ハンドルから位置しているすべてのデータの取得 API のデータの局所性の利点がありますができず、読み取り専用データへの間接参照の追加レベルの局所性の利点がありますから読み取り専用データへの拡張します。 読み取り専用データの一部は、局所性の利点がありますが、データの重複を正当化する場合、各コンテキスト ハンドルのリージョンにレプリケートできます。 ただし、各遅延コンテキスト ハンドルをサポートするメモリと見なされます、premium のような価値のあるデータは、ハンドルから隣接していないが比較的大きなおよびからはアクセスできないとして頻繁に他のデータとしてそのデータを移動するとあります。 理想的には、各遅延コンテキスト ハンドルに関連付けられているデータの種類は頻度の高いデータはすべてとにかく;そのため、データを必要な再配置を検討するのに十分な大きさはできません。 当然ながら、ドライバーは、これらの競合する動機を分散する必要があります。

ドライバーのデータの設計を Direct3D のバージョン 10 と互換性が効率的に行うには、実装では、まだいない分岐読み取り専用データにあります連続した (と後からも分離されます)、イミディ エイト コンテキスト ハンドル データ。 ドライバーは、この設計を使用している場合、ドライバーはキャッシュ ラインの埋め込みはイミディ エイト コンテキスト ハンドルと読み取り専用データの間で必要なことに注意である必要があります。 スレッドは、頻繁に (ない場合は同時に) 各コンテキスト ハンドルのデータを操作があります、ため、偽共有のペナルティは、キャッシュ ラインのパディングを使用しない場合、イミディ エイト コンテキスト ハンドルのデータと遅延コンテキスト ハンドルのデータ間に発生します。 ドライバーの設計を理解している必要がありますマニフェストは、ポインターが確立されているし、コンテキストの間で定期的にスキャン場合偽共有の罰則がメモリ領域を処理します。

Direct3D のランタイムは、ローカル処理の遅延のコンテキストの次の Direct3D 11 DDI を使用します。

-   [ **CheckDeferredContextHandleSizes** ](https://msdn.microsoft.com/library/windows/hardware/ff539388)関数遅延コンテキスト ハンドルのハンドルのデータを保持するドライバー プライベート メモリ空間のサイズを確認します。

-   [ **CalcDeferredContextHandleSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538272)関数は、遅延のコンテキストのメモリの領域のサイズを決定します。

Direct3D、ランタイム、ドライバーで必要とされる遅延コンテキスト ハンドルのサイズを取得する場合は、上記の DDI 関数を使用する必要があります。 ランタイムが呼び出すイミディ エイト コンテキスト オブジェクトの作成後すぐに[ **CalcDeferredContextHandleSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538272)ドライバーをドライバーが必要とするストレージ領域の量を照会するにはこのオブジェクトに遅延コンテキスト ハンドルを満たします。 ただし、Direct3D API は、一意のハンドルの数のサイズを決定することでその CLS メモリ アロケーターを調整する必要があり、その値がアクセスされます。ランタイムが呼び出す、ドライバーの[ **CheckDeferredContextHandleSizes** ](https://msdn.microsoft.com/library/windows/hardware/ff539388)この情報を取得します。 そのため、デバイスのインストール時に、API 遅延コンテキスト ハンドルのサイズの配列によって要求二重ポーリングします。 最初のポーリング要求数のサイズが返されるは、2 つ目のポーリング渡します配列の各サイズの値を取得中にすることです。 ドライバーは、どの程度メモリのために必要などのハンドル型と共に、ハンドルを満たすを示す必要があります。 ドライバーは、特定のハンドル型に関連付けられている複数のサイズを返すことができます。 ただし、これまでの値を返すドライバーの定義されていない**CalcDeferredContextHandleSize**でもそれに応じて返されたされません、 **CheckDeferredContextHandleSizes**配列。

DDI ハンドルを作成する場合とは、遅延のコンテキストでの create メソッドが使用されます。 たとえば、確認、 [ **CreateBlendState (D3D10\_1)** ](https://msdn.microsoft.com/library/windows/hardware/ff540597)と[ **DestroyBlendState** ](https://msdn.microsoft.com/library/windows/hardware/ff552745)関数。 HDEVICE、必然的コンテキストを指して、適切な遅延 (従来は、イミディ エイト コンテキスト)。その他の構造体の CONST ポインターは**NULL** (オブジェクトと仮定すると依存関係を持たない); と、D3D10DDI\_HRT\*ハンドルが、D3D10DDI\_H\*対応するハンドルイミディ エイト コンテキスト オブジェクト。

依存関係のあるオブジェクト (たとえば、ビュー上にある依存関係を対応するリソース)、依存関係のハンドルを提供する構造体のポインターが**NULL**します。 ただし、構造体の唯一の有効なメンバーには、依存関係のハンドルです。一方、残りのメンバーがゼロで埋められます。 例として、 [ **D3D11DDIARG\_CREATESHADERRESOURCEVIEW** ](https://msdn.microsoft.com/library/windows/hardware/ff542073)ドライバーの呼び出しでポインター [ **CreateShaderResourceView(D3D11)**](https://msdn.microsoft.com/library/windows/hardware/ff540708)関数にすることはできません**NULL**遅延のコンテキストで、ランタイムがこの関数を呼び出すとします。 この CreateShaderResourceView(D3D11) 呼び出しで、ランタイムは、リソースが適切なローカル コンテキスト ハンドルを割り当てます、 **hDrvResource** D3D11DDIARG のメンバー\_CREATESHADERRESOURCEVIEW します。 D3D11DDIARG のメンバーの残りの部分\_CREATESHADERRESOURCEVIEW がゼロで埋められます。

次の例のコードは要求と即時と遅延のコンテキストを作成するユーザー モードのディスプレイ ドライバーへの呼び出しを遅延コンテキストの最初の使用を Direct3D ランタイム アプリケーションの変換方法作成します。 アプリケーションの呼び出しを**ID3D11Device::CreateTexture2D** 「リソースの作成」の次のセクションでは、ランタイム コードを開始します。 アプリケーションの呼び出しを**ID3D11Device::CopyResource** 「コンテキスト リソース使用量の遅延」の次のセクションでは、ランタイム コードを開始します。

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

### <a name="span-idissueswithpfnseterrorcbspanspan-idissueswithpfnseterrorcbspanissues-with-pfnseterrorcb"></a><span id="issues_with_pfnseterrorcb"></span><span id="ISSUES_WITH_PFNSETERRORCB"></span>PfnSetErrorCb に関する問題

どの作成関数は、エラー コードは、Direct3D のバージョン 11 スレッド処理モデルの理想的なされている場合を返します。 すべての作成関数を使用して[ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)ドライバーからエラーを取得するコードを返します。 Direct3D のバージョン 10 ドライバー モデルとの互換性を最大化するには、新しい DDI はエラー コードが発生しないを返す関数を作成します。 代わりに、ドライバーが統一されたデバイス/イミディ エイト コンテキスト D3D10DDI を使用して続ける必要があります\_HRTCORELAYER 処理**pfnSetErrorCb**作成関数の中にします。 ドライバーは、コマンドのリストをサポートする、ドライバー、適切な使用する必要があります**pfnSetErrorCb**対応するコンテキストに関連付けられています。 遅延コンテキスト エラーを遅延コンテキストの特定の呼び出しに移動する必要があります、 **pfnSetErrorCb**と対応するハンドルを使用します。

遅延コンテキストを返すことができます E\_呼び出しを通じて OUTOFMEMORY [ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929) D3DDDIERR を以前のみ許可されている DDI 関数から\_DEVICEREMOVED (など[**描画**](https://msdn.microsoft.com/library/windows/hardware/ff556120)、 [ **SetBlendState**](https://msdn.microsoft.com/library/windows/hardware/ff569527)など)、遅延コンテキスト メモリの需要の高まりにより DDI 関数を呼び出すごとに永続的であるためです。 Direct3D API では、このような失敗の場合、部分的に構築されたコマンドの一覧を効果的に解決されると、ドライバーを支援するために、ローカル コンテキストの削除をトリガーします。 アプリケーションは、コマンドの一覧を記録するかを判断を継続します。ただし、アプリケーション、最終的に呼び出すと、 **FinishCommandList**関数、 **FinishCommandList** E のエラー コードが返らない\_OUTOFMEMORY します。

 

 





