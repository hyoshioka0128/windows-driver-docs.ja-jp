---
title: 遅延コンテキストに対するマッピング
description: 遅延コンテキストに対するマッピング
ms.assetid: 29c44639-ea5e-4255-8e8c-f6d5e3af0dfb
keywords:
- Direct3D のバージョン 11 WDK Windows 7 を表示する遅延のコンテキストのマッピング
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 を表示する遅延のコンテキストのマッピング
- 遅延コンテキスト WDK Windows 7 のディスプレイ上のマッピング
- 遅延コンテキスト WDK Windows Server 2008 R2 の表示、DDI 関数を除く上のマッピング
- 遅延コンテキスト WDK Windows 7 を表示するマップ
- 遅延コンテキスト WDK Windows Server 2008 R2 を表示するマップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f9aa515f6d60a1ce5681a6ab39b12c900e0890
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370130"
---
# <a name="mapping-on-deferred-contexts"></a>遅延コンテキストに対するマッピング


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

ランタイムは、動的なリソースをマップできます (ドライバーの呼び出しを通じて[ **ResourceMap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)関数) 遅延のコンテキストで、Direct3D とバージョン 11 API により、マップの動的の最初の使用リソースでは、以前の内容を破棄します。 最適なオプションでは、継続的に、元の動的なリソースを使用して経由で各破棄で新しい動的なリソースを作成します。 このエイリアス化されたリソースの作成が必要です、即時のタイムラインに動的な仮想リソースに行われる操作に影響する遅延のコンテキストのタイムラインに動的な仮想リソースに実行される操作を許可するにはコンテキスト。 ただし、遅延のコンテキストは最終的に、ドライバーの呼び出し中に actualized は操作の記録で単[ **CommandListExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)関数。 動的リソースの使用し、アプリケーションの元の意図は保持されますが、GPU にアクセス可能なメモリの書き込み結合は、アプリケーションに提供されます (1 つ使用するためのメモリの最適化は、CPU のアップロード) します。

各リソース マップには、エイリアス化されたリソースに直接ポインターを提供できます。 この型のエイリアスを実装する記録遅延のコンテキストでは負担がかかります。 たとえば、遅延のコンテキストの記録では、テクスチャのエイリアスを作成する新しいビューを必要があります。 ドライバーのエイリアスとの統合は、必要なを行うには妥当と思われます。 コマンドの一覧が実行されたときに、(マップ破棄呼び出しを満たす) にリソースを作成する最後のコンテキストでローカルとイミディ エイト コンテキストは、動的リソースをバックアップする「現在」のリソースとして代わりに使用する必要があります。

ドライバーへの呼び出し[**リソース**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopy)動的リソースにリソースをコピーする関数は、マップ破棄の呼び出し後に、遅延のコンテキストと後のイミディ エイト コンテキストの両方がサポートする必要があります、ドライバーへの呼び出し[ **CommandListExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)関数の場合、遅延コンテキストのローカル リソースが「現在」のリソースのイミディ エイト コンテキストのバージョンにスワップが理想的です。 ドライバーへの呼び出し**リソース**動的リソースの変換先を持つ関数が頻繁に使用しないように、コピー オン ライト メカニズムを使用する必要があります。 場合**リソース**が呼び出されたか、動的リソース マップ破棄呼び出しの後に遅延のコンテキストか、または新しいリソースを現在コマンド一覧のローカル リソースを保持するイミディ エイト コンテキストに影響をする必要がありますが概念的には、コピーの新しい変換先を提供する割り当てられ、古いリソースを新しいリソースにコピーする必要があります (操作の場合、 [ **ResourceCopyRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopyregion))。

 

 





