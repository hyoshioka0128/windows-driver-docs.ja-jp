---
title: ノードの制御ピンの決定
description: ノードの制御ピンの決定
ms.assetid: be1236e2-c710-4833-863e-54e826e53f92
keywords:
- メソッドは、WDK BDA、暗証番号 (pin) を制御するノードを設定します。
- プロパティは、WDK BDA、暗証番号 (pin) を制御するノードを設定します。
- WDK BDA 暗証番号 (pin) を制御します。
- ノードの制御のピン留め WDK BDA
- WDK BDA 配列
- 暗証番号 (pin) コント ローラー WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dfad0bbad0970d7f1d29c912fe880423b9fc0c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360175"
---
# <a name="determining-the-controlling-pin-of-a-node"></a>ノードの制御ピンの決定





フィルターと pin とは異なりノードには、リング 3 でのアプリケーション アクセスできる、関連付けられているファイル ハンドルがありません。 ノードがフィルター内での内部コンポーネントであるため、存在する場所に、フィルターの入力と出力ピンの間。 ネットワーク プロバイダーを使用するには、どのフィルター pin を確認し、暗証番号 (pin) を使用して、ノードにアクセスする必要があります。 このフィルターの暗証番号 (pin) には、そのノードの制御の暗証番号 (pin) が呼び出されます。 ネットワーク プロバイダーが、KSPROPERTY をクエリ フィルターの BDA テンプレート接続リスト内の各ノードの制御の暗証番号 (pin) を決定する\_BDA\_制御\_PIN\_の ID プロパティ、 [KSPROPSETID\_BdaTopology](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-bdatopology)プロパティ セット。 BDA ミニドライバーを呼び出し、 [ **BdaPropertyGetControllingPinId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertygetcontrollingpinid)ノードごとに関数をサポートします。 この呼び出しで、ミニドライバーはへのポインターを渡す、 [ **KSP\_BDA\_ノード\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ns-bdamedia-_ksp_bda_node_pin)構造体。 この構造体は、特定のノード型と、フィルターの入力のペアを制御するピンと出力ピンを取得するプロパティの要求を識別します。 BDA サポート ライブラリは、ノード型を制御するピンの識別子を返します。

BDA ミニドライバーが、KSPROPERTY を通常インターセプトされなく\_BDA\_制御\_PIN\_ID プロパティ。 ミニドライバーが自動的にディスパッチ、 **BdaPropertyGetControllingPinId** 、KSPROPSETID から関数をサポートして\_BdaTopology プロパティ セット。 参照してください[BDA デバイス トポロジを決定する](determining-bda-device-topology.md)詳細についてはします。

サポート ライブラリが BDA ミニドライバーへのポインターをサポート ライブラリを提供するために、制御の暗証番号 (pin) の識別子を決定するすべての作業を行う、 [ **BDA\_フィルター\_テンプレート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/ns-bdasup-_bda_filter_template) BDA ミニドライバーは、運用を開始時に構造体します。 参照してください[開始 BDA ミニドライバー](starting-a-bda-minidriver.md)詳細についてはします。 通知 BDA サポート ライブラリ BDA に含まれる情報を制御するピンを確認する方法の BDA ミニドライバー\_フィルター\_テンプレート。 この情報には、次の内容が含まれます。

-   接続の配列。 この配列は、 [ **KSTOPOLOGY\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection)フィルター内でか、フィルターとの間、表現のノードと pin の間のすべての使用可能な接続の種類を提供する配列を作成できますフィルターに隣接します。 参照してください[接続トポロジのマッピング](mapping-connection-topology.md)、KSTOPOLOGY の詳細については\_接続の配列。

-   共通値の配列。 ジョイントは、トポロジ内のポイントを別の出力を 1 つまたは複数のパスに分割します。 1 つの入力または 1 つ以上の入力が 1 つの出力パスに結合します。 ジョイントに渡された値が、KSTOPOLOGY 内の要素のインデックスに対応\_接続の配列。 ほとんどのトポロジは、1 つだけジョイント必要があります。

-   配列の[ **BDA\_PIN\_ペアリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/ns-bdasup-_bda_pin_pairing)構造体。 これらの構造は、入力と出力ピンの種類や、フィルターを作成できる入力型のインスタンスの最大数、フィルターを作成できる出力型のインスタンスの最大数を特定します。 これらの構造体には、入力と出力ピンの間の結合値の配列へのポインターも含まれます。 参照してください[BDA ミニドライバーを開始](starting-a-bda-minidriver.md)、BDA の詳細については\_PIN\_ペアリングの配列。

次の図は、サポート ライブラリが特定のノードを制御するフィルターの暗証番号 (pin) を決定する方法を示しています。

![サポート ライブラリが特定のノードを制御するフィルターの暗証番号 (pin) を決定する方法を示す図](images/bdajoint.png)

 

 




