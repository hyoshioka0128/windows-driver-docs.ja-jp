---
title: BDA フィルターの初期化
description: BDA フィルターの初期化
ms.assetid: 716978f5-4bdd-4673-8c4a-14dc76947fba
keywords:
- BDA ミニドライバー WDK AVStream, フィルター初期化
- BDA フィルターの初期化
- 初期フィルターインスタンス WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc6e63dcd775ce42df8f0ba7ca82dda00b1d26e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845575"
---
# <a name="initializing-a-bda-filter"></a>BDA フィルターの初期化





ネットワークプロバイダーフィルターでは、ネットワークプロバイダーがフィルターグラフを作成するときに、BDA デバイスの初期フィルター記述子の作成ディスパッチルーチンを使用して、BDA デバイスの初期フィルターインスタンスを作成します。 この初期フィルター記述子はフィルターファクトリとして設定され、bda デバイスの開始時に bda デバイスの BDA フィルターテンプレートに関連付けられていました。 最初に作成されるフィルターインスタンスは、少なくとも1つの入力を公開する必要があります。 通常、最初のフィルターインスタンスは、初期フィルター記述子で使用可能な入力ピンごとに入力ピンを公開しますが、出力ピンは公開しません。 詳細について[は、「BDA ミニドライバーを開始する](starting-a-bda-minidriver.md)」および「[ディスパッチテーブルを作成](creating-dispatch-tables.md)する」を参照してください。

BDA フィルターの create ルーチンは、フィルターオブジェクトにメモリを割り当て、フィルターオブジェクトのメンバー変数を設定する必要があります。その後、 [**BdaInitFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter) support 関数を呼び出して、フィルターインスタンスを初期化します。 この呼び出しでは、BDA フィルターの create ルーチンは、作成する初期フィルターの[**Ksk フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter)構造へのポインターと、フィルターのの可能性を記述する[**bda\_フィルター\_テンプレート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template)構造へのポインターを渡します。初期フィルターインスタンスのテンプレートトポロジ。

 

 




