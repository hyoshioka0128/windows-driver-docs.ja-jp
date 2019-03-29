---
title: NDKPI リスナー、コネクタ、およびエンドポイント
description: このセクションでは、NDKPI リスナー、コネクタ、およびエンドポイント、および参照カウントのコネクタとエンドポイントについて説明します。
ms.assetid: 956D3550-11C8-48D0-BCF4-9027515C7C0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 192f287d210db880df875b6a8e8a6daeb737bf19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572984"
---
# <a name="ndkpi-listeners-connectors-and-endpoints"></a>NDKPI リスナー、コネクタ、およびエンドポイント


NDK コンシューマーを呼び出すことによって、NDK コネクタの接続、 *NdkConnect* ([*NDK\_FN\_CONNECT*](https://msdn.microsoft.com/library/windows/hardware/hh439865)) または*NdkConnectWithSharedEndpoint* ([*NDK\_FN\_CONNECT\_WITH\_SHARED\_エンドポイント*](https://msdn.microsoft.com/library/windows/hardware/hh439868)) 関数。

接続されている状態にある各コネクタでは、確立された NDK 接続のローカル側を表す基になるエンドポイントにもあります。

-   コネクタを確立するには、NDK リスナー経由で着信接続を自動的にそのまま使用して、ローカルの暗黙的なエンドポイントとしてリスナーの暗黙的なエンドポイントを継承します。
-   コネクタを介して接続されている、 *NdkConnect*関数には、独自の専用暗黙のローカル エンドポイント。
-   コネクタを介して接続されている、 *NdkConnectWithSharedEndpoint*関数には、明示的なローカル エンドポイント経由で接続している他のコネクタを共有できる、 *NdkConnectWithSharedEndpoint*関数。

NDK プロバイダーがなんらかの各暗黙的または明示的なエンドポイントの参照カウントを保持し、エンドポイントをリリースする必要があります (つまり、もう一度使用する利用可能なアドレスとポートをマークする)、参照カウントがゼロになったとき。

### <a name="reference-counting-for-non-shared-endpoints"></a>エンドポイントの (非共有) に対して参照カウント

コンシューマーを呼び出すと、 *NdkListen* ([*NDK\_FN\_リッスン*](https://msdn.microsoft.com/library/windows/hardware/hh439902)) 関数、プロバイダーは、暗黙的なエンドポイントを作成します。 この暗黙的なエンドポイントでプロバイダーは次のように参照カウントを維持する必要があります。

-   エンドポイントの参照カウントには、リスナー自体の参照を追加します。
-   各リスナーで受け入れられるコネクタへの参照を追加します。
-   リスナーで受け入れられた以前コネクタが閉じられたときに、参照を削除します。
-   リスナー自体が閉じられたときに、参照を削除します。
    **注**  のすべてのコネクタが閉じられるまで、リスナーを閉じることができません。

     

-   参照カウントがゼロに返されるときに、エンドポイントをリリースします。 (これは大文字と小文字が既に閉じられているリスナーとのすべてのコネクタが、リスナー経由で許可される場合のみ) です。
-   リスナーを閉じるだけは、エンドポイントを解放しませんまだ閉じていない承認済みのコネクタがある限り。 つまり、その新しい*NdkListen*、 *NdkConnect*、および*NdkConnectWithSharedEndpoint*要求は、このようなすべての接続まで、同じローカル アドレスとポートは失敗閉じられます。 リスナーを閉じる要求が保留中も残ることに注意してください。 このようなすべての接続が閉じられるまで (で説明する/後続処理の継続元の規則により[NDKPI オブジェクトの有効期間の要件](ndkpi-object-lifetime-requirements.md))。 (その終了要求が保留中、新しい接続を受け入れるできません)、終了要求が発行されるとすぐに、プロバイダーは、リスナーでさらに着信接続を拒否する必要があります。

### <a name="reference-counting-for-connectors"></a>参照コネクタのカウント

コンシューマーを呼び出すと*NdkConnect*プロバイダーを作成し、暗黙的なエンドポイント。 この暗黙的なエンドポイントの場合、プロバイダーが必要です。

-   コネクタでの参照を追加します。 1 つだけのコネクタ、そのため 1 つだけ参照があります。
-   コネクタが閉じられたときに、エンドポイントへのコネクタの参照を削除します。
-   その参照されなくなったときにエンドポイントをリリースします。

### <a name="reference-counting-for-shared-endpoints"></a>共有のエンドポイントに対する参照カウント

コンシューマーを呼び出すと*NdkConnectWithSharedEndpoint*プロバイダーは、明示的な共有エンドポイントを作成します。 この明示的な共有エンドポイント プロバイダー必要があります。

-   共有のエンドポイントの参照カウントに共有エンドポイントそのものへの参照を追加します。
-   その共有エンドポイント経由で接続されている各コネクタへの参照を追加します。
-   共有エンドポイント経由で接続されているコネクタが閉じられたときに、参照を削除します。
-   エンドポイント参照カウントのリリースでは、0 を返します。 (この場合、共有のエンドポイントと共有エンドポイント経由で接続されているすべてのコネクタが終了した場合にします。)
-   単に、共有のエンドポイントを終了しても、エンドポイントは解放されませんまだ終了していない以前接続されているコネクタがある限り。 つまり、その新しい*NdkListen*、 *NdkConnect*、および*NdkConnectWithSharedEndpoint*要求は、このようなすべての接続まで、同じローカル アドレスとポートは失敗閉じられます。 共有のエンドポイントに要求が保留中も残ることに注意してください。 このようなすべての接続が閉じられるまで (で説明する/後続処理の継続元の規則により[NDKPI オブジェクトの有効期間の要件](ndkpi-object-lifetime-requirements.md))。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






