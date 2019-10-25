---
title: ノードの制御ピンの決定
description: ノードの制御ピンの決定
ms.assetid: be1236e2-c710-4833-863e-54e826e53f92
keywords:
- メソッド設定 WDK BDA、ノード制御 pin
- プロパティ設定 WDK BDA、ノード制御 pin
- pin WDK BDA の制御
- pin を制御するノード (WDK)
- 配列 WDK BDA
- pin コントローラー WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ed66297709935be45fa47c5192d63fa831a9ed1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844786"
---
# <a name="determining-the-controlling-pin-of-a-node"></a>ノードの制御ピンの決定





フィルターや pin とは異なり、ノードには、リング3のアプリケーションがアクセスできるファイルハンドルが関連付けられていません。 ノードはフィルター内の内部コンポーネントであるため、フィルターの入力ピンと出力ピンの間に存在します。 ネットワークプロバイダーは、使用するフィルター pin を決定してから、その pin を使用してノードにアクセスします。 このフィルターピンは、そのノードの制御ピンと呼ばれます。 フィルターの BDA テンプレート接続リストの各ノードについて制御する pin を決定するために、ネットワークプロバイダーは、ksk プロパティ\_BDA\_をクエリします。これは、 [Kspropsetid\_](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-bdatopology)の\_PIN\_ID プロパティを制御します。プロパティセット。 さらに、BDA ミニドライバーは、各ノードの[**BdaPropertyGetControllingPinId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetcontrollingpinid) support 関数を呼び出します。 この呼び出しでは、ミニドライバーは[**KSP\_BDA\_ノード\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-_ksp_bda_node_pin)構造へのポインターを渡します。 この構造体は、特定のノードタイプの制御ピンと、フィルターの入力ピンと出力ピンのペアを取得するプロパティ要求を識別します。 BDA サポートライブラリは、ノード型の制御ピンの識別子を返します。

通常、BDA ミニドライバーは\_PIN\_ID プロパティを制御する KSK プロパティ\_BDA\_をインターセプトしません。 ミニドライバーは、 **BdaPropertyGetControllingPinId** support 関数を KSK propsetid\_BdaTopology プロパティセットから自動的にディスパッチします。 詳細については、「 [BDA デバイストポロジの決定](determining-bda-device-topology.md)」を参照してください。

サポートライブラリでは、bda ミニドライバーを[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template)使用すると、コントロールピンの識別子を決定するすべての作業を実行できます。これは、bda ミニドライバーが、bda操作を開始しました。 詳細について[は、「BDA ミニドライバーの開始](starting-a-bda-minidriver.md)」を参照してください。 Bda ミニドライバーは、bda サポートライブラリに対して、BDA\_FILTER\_テンプレートに含まれている情報を使用した pin の制御方法を通知します。 この情報には、次の内容が含まれます。

-   接続の配列。 この配列は、フィルター内またはフィルターと隣接するフィルターの間で可能な、ノードとピンの種類の間のすべての接続の表現を提供する[**Kstopology\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)配列です。 KSTOPOLOGY\_接続配列の詳細については、「[接続トポロジのマッピング](mapping-connection-topology.md)」を参照してください。

-   結合値の配列。 ジョイントは、1つの入力が異なる出力への1つまたは複数のパスに分割されるトポロジのポイントで、1つの出力パスへの1つ以上の入力結合です。 ジョイントに指定された値は、KSTOPOLOGY\_接続配列内の要素のインデックスに対応します。 ほとんどのトポロジには、結合が1つだけあります。

-   \_ペアリング構造体の[**BDA\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_pin_pairing)の配列。 これらの構造体は、入力ピンと出力ピンの種類、フィルターで作成できる入力型のインスタンスの最大数、およびフィルターに作成できる出力の種類のインスタンスの最大数を識別します。 これらの構造体には、入力ピンと出力ピン間の結合値の配列へのポインターも含まれます。 BDA\_ピン\_配列のペアリングの詳細については、「 [bda を開始する](starting-a-bda-minidriver.md)」を参照してください。

次の図は、サポートライブラリによって、特定のノードを制御するフィルターピンがどのように決定されるかを示しています。

![特定のノードを制御するフィルターの pin をサポートライブラリが決定する方法を示す図](images/bdajoint.png)

 

 




