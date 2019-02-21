---
title: NetworkDirect 切断スキーム
description: このセクションには、NetworkDirect の切断スキームがについて説明します
ms.assetid: A7973588-5AED-494E-92CA-D5EFB2C7950A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1a96c82c7ce74f3d9d36b4eff463ff11978b018
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548653"
---
# <a name="networkdirect-disconnect-scheme"></a>NetworkDirect 切断スキーム


ここで説明されているスキームは、両方に適用されます[NDSPI](https://msdn.microsoft.com/library/cc904391)バージョン 2 と[NDKPI](network-direct-kernel-programming-interface--ndkpi-.md)します。 次の用語が使用されます。

-   ND は NDSPI または NDK を参照するために使用します。
-   *NdDisconnect* ND コンシューマーは正常な切断を開始するには、関数呼び出しを参照するために使用します。 これは、NDSPI [ **INDConnector::Disconnect**](https://msdn.microsoft.com/library/cc904364)します。 NDKPI *NdkDisconnect* ([*NDK\_FN\_切断*](https://msdn.microsoft.com/library/windows/hardware/hh439885))。
-   *NdDisconnectIndication* ND プロバイダーが正常に受信すると、ND プロバイダーによって、ND コンシューマーに配信を示す値を参照するために使用または何らかの理由 (以外のローカル接続が中止されたことを検出した場合、ピアから切断NDK コンシューマーの発行などの開始を所有*NdDisconnect*または*NdCloseConnector*)。

以下は、A と B は、ND 接続の両側を参照してください。 A のコンシューマーが ND コンシューマー側に、プロバイダー、側に、ND プロバイダーを参照およびコンシューマー B/プロバイダー B が B. 側でこれらの同じエンティティを指す同様にA のコンシューマーを呼び出すと*NdDisconnect*、プロバイダーの A を正常に送信する必要がありますが B の側に通知を切断し、コンシューマー A の完了*NdDisconnect*要求のみの両方の次の条件が発生した場合。

-   次のいずれかを行います。
    -   正常な切断通知 B から受信した (A のコンシューマーが正常に完了につながる*NdDisconnect*)、または
    -   接続の中断やタイムアウトなど、エラーが発生しました (A のコンシューマーにつながる*NdDisconnect*エラーで完了する)。
-   (サイレント成功フラグで投稿された作業要求 DMA アクティビティ) を含む QP 上のすべての DMA アクティビティが終了しました。

プロバイダ B が正常に受信すると、A から通知を切断またはことは、接続が中止され、B のプロバイダーが提供する必要がありますが検出された*NdDisconnectIndication*コンシューマー B コンシューマー B が呼び出されていない場合に*NdDisconnect*プロバイダー B は既ににします。 正常な受信後、通知を切断または中止イベントがローカルのコンシューマーを開始すると競合できます*NdDisconnect*、ローカルのコンシューマーが処理する準備をする必要があります、 *NdDisconnectIndication*ローカルのコンシューマーの呼び出し後に到着した*NdDisconnect*します。 なお、 *NdDisconnectIndication*作業要求が完了に関して一切の保証を行いません。

コンシューマーでは、切断された QP またはコネクタを再利用することはできません。

NetworkDirect は、半分に閉じられた接続の概念はありません。 1 回*NdDisconnect*が完了した、接続が閉じられる完全 (成功または失敗) を使用します。

コンシューマーは呼び出す必要があります通常*NdDisconnect*発信側キューにポストされた、すべての作業要求用の入力候補を取得した後にのみです。 それ以外の場合、 *NdDisconnect* true 正常な切断していない可能性があります。 プロバイダーにする必要はありません、コンシューマーがこのような作業要求未処理の場合は正常なサポートを切断します。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






