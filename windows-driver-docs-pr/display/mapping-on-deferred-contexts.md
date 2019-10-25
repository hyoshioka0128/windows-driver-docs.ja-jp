---
title: 遅延コンテキストに対するマッピング
description: 遅延コンテキストに対するマッピング
ms.assetid: 29c44639-ea5e-4255-8e8c-f6d5e3af0dfb
keywords:
- Direct3D version 11 WDK Windows 7 display、遅延コンテキスト、マッピング
- Direct3D バージョン 11 WDK Windows Server 2008 R2 の表示、遅延コンテキスト、マッピング
- 遅延コンテキストでのマッピング WDK Windows 7 ディスプレイ
- 遅延コンテキストでのマッピング WDK Windows Server 2008 R2 表示 (DDI 関数を除く)
- 遅延コンテキスト WDK Windows 7 display、mapping
- 遅延コンテキスト WDK Windows Server 2008 R2 表示、マッピング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d4476c6c8e3be137235a0b949a0c4a9132ac35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840576"
---
# <a name="mapping-on-deferred-contexts"></a>遅延コンテキストに対するマッピング


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

ランタイムは、遅延コンテキストで (ドライバーの[**Resourcemap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)関数の呼び出しを通じて) 動的リソースをマップできます。これは、Direct3D VERSION 11 API によって、マップされた動的リソースの最初の使用によって前の内容が破棄されるためです。 最善の方法は、元の動的リソースを使用して継続的に破棄するたびに、新しい動的リソースを作成することです。 このエイリアスが設定されたリソースの作成は、遅延コンテキストのタイムラインで仮想動的リソースに対して実行される操作が、直接のタイムラインで仮想動的リソースに対して実行される操作に影響しないようにするために必要です。関連. 遅延コンテキストは、ドライバーの[**Commandlistexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)関数の呼び出し中に最終的に処理される操作を記録するだけであることに注意してください。 動的リソースが使用されると、アプリケーションの本来の目的が維持され、書き込みが可能な GPU アクセス可能なメモリがアプリケーションに提供されます (つまり、メモリはシングルユースの CPU アップロード用に最適化されます)。

各リソースマップは、エイリアス化されたリソースに直接ポインターを提供できます。 この種類の別名を実装するために、遅延コンテキストの記録には追加の負担があります。 たとえば、遅延コンテキストの記録では、エイリアス化されたテクスチャ用に新しいビューを作成する必要がある場合があります。 ドライバーのエイリアスとの統合が必要であり、そうでないように思えます。 コマンドリストを実行するときは、(マップの破棄呼び出しを満たすために) 最後に作成されたコンテキストローカルリソースを、イミディエイトコンテキストの動的リソースをバックする "現在" のリソースとして置き換える必要があります。

動的リソースにリソースをコピーするためのドライバーの[**ResourceCopy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopy)関数への呼び出しは、遅延コンテキスト、マップの破棄呼び出しの後、およびドライバーの[**commandlistexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)の呼び出し後のイミディエイトコンテキストでもサポートされている必要があります。関数。ローカル遅延コンテキストリソースは、"現在" のリソースの直接コンテキストバージョンにスワップされるのが理想的です。 動的リソースの変換先を使用したドライバーの**ResourceCopy**関数の呼び出しは、頻繁には使用されないため、書き込み時のコピー機能を使用する必要があります。 **ResourceCopy**が呼び出された場合、マップの破棄呼び出しの後、またはコマンドリストのローカルリソースを保持しているイミディエイトコンテキストで、遅延コンテキストの動的リソースのいずれかに影響を与えます。コピーの新しいコピー先を指定し、古いリソースを新しいリソースにコピーする必要があります (操作が[**ResourceCopyRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopyregion)の場合)。

 

 





