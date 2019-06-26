---
title: BDA フィルターの初期化
description: BDA フィルターの初期化
ms.assetid: 716978f5-4bdd-4673-8c4a-14dc76947fba
keywords:
- BDA ミニドライバー WDK AVStream、フィルターの初期化
- BDA フィルターを初期化しています
- 初期フィルター インスタンス WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2cfe00db17856c80fc85579323438242ad7ab58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360687"
---
# <a name="initializing-a-bda-filter"></a>BDA フィルターの初期化





ネットワーク プロバイダーのフィルターでは、BDA デバイスの初期のフィルター記述子の作成のディスパッチ ルーチンを使用して、ネットワーク プロバイダーがフィルター グラフを作成するときに、BDA デバイスの初期フィルター インスタンスを作成します。 この最初のフィルター記述子は、フィルター ファクトリとして設定され、BDA デバイスが開始したときに、BDA デバイス BDA フィルター テンプレートに関連付けられています。 作成される初期フィルター インスタンスには、少なくとも 1 つの入力を公開する必要があります。 通常、初期フィルター インスタンスは、最初のフィルター記述子で可能な各入力ピンの入力のピンを公開しますが、出力ピンを公開しません。 参照してください[開始 BDA ミニドライバー](starting-a-bda-minidriver.md)と[ディスパッチ テーブルを作成](creating-dispatch-tables.md)詳細についてはします。

ルーチンを作成、BDA フィルターのフィルター、そのオブジェクトのメモリを割り当てる必要がありますや、フィルター オブジェクトのメンバー変数を設定する必要がありますし、呼び出す必要があります、 [ **BdaInitFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdainitfilter)を初期化する関数をサポートフィルターのインスタンス。 この呼び出しで BDA フィルターのパスを作成しますルーチンへのポインター、 [ **KSFILTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter)構造を作成する最初のフィルターとへのポインター、 [ **BDA\_フィルター\_テンプレート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/ns-bdasup-_bda_filter_template)初期フィルター インスタンスのフィルターのテンプレートのトポロジのさまざまな可能性を記述する構造体。

 

 




