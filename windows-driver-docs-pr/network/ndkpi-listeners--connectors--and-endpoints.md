---
title: NDKPI リスナー、コネクタ、エンドポイント
description: このセクションでは、NDKPI のリスナー、コネクタ、エンドポイント、およびコネクタとエンドポイントの参照カウントについて説明します。
ms.assetid: 956D3550-11C8-48D0-BCF4-9027515C7C0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd82fbeb957402088d81e7c6c2ca88b8c2ac7815
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831895"
---
# <a name="ndkpi-listeners-connectors-and-endpoints"></a>NDKPI リスナー、コネクタ、およびエンドポイント


NDK コンシューマーは、 *Ndkconnect* ([*ndk\_fn\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)) または*Ndkconnectwithsharedendpoint* ([*ndk\_FN\_CONNECT\_と\_共有\_を呼び出すことにより、ndk コネクタに接続します。エンドポイント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)) 関数。

接続された状態の各コネクタには、確立された NDK 接続のローカルエンドを表す基になるエンドポイントもあります。

-   NDK リスナー経由で受信接続を受け入れることによって確立されたコネクタは、リスナーの暗黙的なエンドポイントをローカルの暗黙的なエンドポイントとして自動的に継承します。
-   *Ndkconnect*関数を介して接続されるコネクタには、独自の専用の暗黙的なローカルエンドポイントがあります。
-   *Ndkconnectwithsharedendpoint*関数を介して接続されているコネクタには、 *ndkconnectwithsharedendpoint*関数を介して接続されている他のコネクタと共有できる、明示的なローカルエンドポイントがあります。

NDK プロバイダーは、暗黙的または明示的なエンドポイントごとに何らかの参照カウントを保持し、エンドポイントを解放する必要があります (つまり、参照カウントが0になったときに、使用可能なアドレスとポートをマークします)。

### <a name="reference-counting-for-non-shared-endpoints"></a>(非共有) エンドポイントの参照カウント

コンシューマーが*Ndklisten* ([*NDK\_FN\_LISTEN*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_listen)) 関数を呼び出すと、プロバイダーは暗黙的なエンドポイントを作成します。 この暗黙的なエンドポイントの場合、プロバイダーは次のように参照カウントを維持する必要があります。

-   リスナー自体の参照をエンドポイントの参照カウントに追加します。
-   そのリスナーで受け入れられる各コネクタの参照を追加します。
-   リスナーで既に受け入れられているコネクタが閉じている場合は、参照を削除します。
-   リスナー自体が閉じられている場合は、参照を削除します。
    すべてのコネクタが閉じられるまでリスナーを閉じることができない  に**注意**してください。

     

-   参照カウントが0に戻ると、エンドポイントが解放されます。 (これは、リスナーと、リスナーで受け入れられたすべてのコネクタが閉じられている場合にのみ発生します)。
-   リスナーを閉じるだけでは、まだ閉じていない承認済みのコネクタが存在する限り、エンドポイントは解放されません。 これは、同じローカルアドレスとポートに対する新しい*Ndklisten*、 *ndklisten*、および*Ndkconnectwithsharedendpoint*要求が、すべての接続が閉じられるまで失敗することを意味します。 このような接続がすべて閉じられるまで、リスナーでのクローズ要求も保留状態のままになります ( [Ndkpi オブジェクトの有効期間要件](ndkpi-object-lifetime-requirements.md)に記載されている継続元/後続規則によります)。 Close 要求が発行されるとすぐに、プロバイダーがリスナーで受信接続を拒否する必要があります (終了要求の保留中に新しい接続が受け入れられないようにするため)。

### <a name="reference-counting-for-connectors"></a>コネクタの参照カウント

コンシューマーが*Ndkconnect*を呼び出すと、プロバイダーによってと暗黙のエンドポイントが作成されます。 この暗黙的なエンドポイントの場合、プロバイダーは次のことを行う必要があります。

-   コネクタによって参照を追加します。 コネクタは1つしか存在しないため、参照は1つだけです。
-   コネクタが閉じられたときに、コネクタのエンドポイントへの参照を削除します。
-   参照が失われたときにエンドポイントを解放します。

### <a name="reference-counting-for-shared-endpoints"></a>共有エンドポイントの参照カウント

コンシューマーが*Ndkconnectwithsharedendpoint*を呼び出すと、プロバイダーは明示的な共有エンドポイントを作成します。 この明示的な共有エンドポイントでは、プロバイダーは次のことを行う必要があります。

-   共有エンドポイント自体の参照を共有エンドポイントの参照カウントに追加します。
-   その共有エンドポイントで接続されている各コネクタの参照を追加します。
-   以前に共有エンドポイント経由で接続されていたコネクタが閉じている場合は、参照を削除します。
-   参照カウントが0に戻るエンドポイントを解放します。 (共有エンドポイントと、共有エンドポイントを介して接続されているすべてのコネクタが閉じられている場合)。
-   共有エンドポイントを閉じるだけでは、まだ閉じていないコネクタが既に接続されている限り、エンドポイントは解放されません。 これは、同じローカルアドレスとポートに対する新しい*Ndklisten*、 *ndklisten*、および*Ndkconnectwithsharedendpoint*要求が、すべての接続が閉じられるまで失敗することを意味します。 共有エンドポイントでのクローズ要求も、このようなすべての接続が閉じられるまで保留状態のままになります (「 [Ndkpi オブジェクトの有効期間の要件](ndkpi-object-lifetime-requirements.md)」に記載されている継続元/後続の規則によります)。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






