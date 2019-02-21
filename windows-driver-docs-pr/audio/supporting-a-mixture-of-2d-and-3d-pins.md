---
title: 2D と 3D のピンの混在をサポート
description: 2D と 3D のピンの混在をサポート
ms.assetid: 26d98eca-b70a-4244-a7c3-d3a19930a96a
keywords:
- ハードウェア アクセラレータ WDK DirectSound、2 D および 3D 混在をピン留め
- オーディオの WDK ミキシング 3D
- WDK のオーディオを混在させる 2D
- ピンの WDK オーディオ、2 D
- ピンの WDK オーディオ、3 D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048f7e3c4a3a3fa6a68f512d8e0f801d3f1745c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552928"
---
# <a name="supporting-a-mixture-of-2d-and-3d-pins"></a>2D と 3D のピンの混在をサポート


## <span id="supporting_a_mixture_of_2d_and_3d_pins"></span><span id="SUPPORTING_A_MIXTURE_OF_2D_AND_3D_PINS"></span>


場合の 2D と 3D のピンを 3D の pin の組み合わせが倍増する、WDM オーディオ ドライバーがサポートする、暗証番号 (pin) を 2D としてその逆を使用します。 DirectSound は、2 D の pin を必要とする場合、ドライバーから使用できる場合、そのため、未使用の 3D pin を置き換える、できます。 DirectSound は、3 D の pin を必要とする場合、続行を検索中に発生した、2 D のピンを無視して、3 D pin が見つかるまで、暗証番号 (pin) のインスタンスのドライバーの一覧を検索します。 DirectSound は、それらが表示されるその要件を満たす暗証番号 (pin) のインスタンスが見つかるまで順番にピン留めするファクトリのドライバーの一覧を確認します。

2D-pin の数を報告するときに、ドライバーは 2D pin インスタンスの数と 3D pin インスタンスの数を指定する必要があります。 3D-pin の数を報告するときに、ドライバーは 2D のピンを無視して、3D pin インスタンスの数のみを指定する必要があります。

Microsoft Windows 2000 および Windows 98 に分散された DirectSound バージョンでは、2 D および 3D の pin の組み合わせを公開するピン留めするファクトリを処理するときは既知の問題があります。DirectSound 2D 暗証番号 (pin) のインスタンスの数と 3D の暗証番号 (pin) のインスタンスの数をある 3D ピンの数が正しく報告されません。 この問題を回避策では、2 つの別々 の pin ファクトリに 2D および 3D のピンを分離ができるように、ドライバーを作成します。 1 つのファクトリは、のみ 2D のピンと他の工場出荷時の 3D のみを公開しますピンを公開します。

WDM ドライバー、DirectSound は 2 つのファクトリから 2D および 3D ピンの数の合計として 2D-pin の数を正しく報告し、1 つの 3D pin ファクトリから 3D ピンの数として 3D-pin の数を正しく報告します。 2D と 3D のピンの個別のファクトリを公開するときに、ドライバーは 3D pin 工場出荷時の前に、2 D pin ファクトリを一覧表示する必要があります。 これは、DirectSound は 2D の pin を探して、見つかると、最初の 2D または 3D の pin を使用するために必要と DirectSound ドライバーがそれらに一覧の順序でピン留めするファクトリを確認します。 ドライバーでは、まず、3 D のファクトリが表示されている場合のリスクがありますが DirectSound 2D の pin の代わりにそれらを不必要を使用して 3D ピンの提供が消費されます。

要約すると、ドライバーが 2D と 3D の pin の組み合わせを公開している場合、DirectSound の以前のバージョンで正常に動作するこれらのルールする必要がありますに従います。

-   2 つの別々 の pin ファクトリの 2D および 3D のピンをそれぞれ提供します。

-   3D pin factory 事前 2D pin ファクトリの一覧を表示します。

これらの回避策では、DirectSound の以降のバージョンで必要ありません。 以降では Windows Me、Windows XP では、上記で説明した問題は固定されています。 それも固定 DirectSound 8 は、Windows の以前のバージョンで使用するために再配分されます。 この修正により、ドライバーは、ピンが 1 つの工場出荷時の 2D および 3D のピンを組み合わせることができますに安全と DirectSound は 2D と 3D ピンの数を正しく報告します。 また、この DirectSound は、2 D の pin を必要とする場合は、暗証番号 (pin) のすべての工場から 2D のピンの提供の最後に達する場合にのみ 2D の pin の代わりに 3D に暗証番号 (pin) には使用します。

 

 




