---
title: NetworkDirect 切断スキーム
description: このセクションでは、NetworkDirect 切断スキームについて説明します。
ms.assetid: A7973588-5AED-494E-92CA-D5EFB2C7950A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5aa61dc132426049d7e3f1169434b5b90ecf0393
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827127"
---
# <a name="networkdirect-disconnect-scheme"></a>NetworkDirect 切断スキーム


ここで説明するスキームは、 [Ndspi](https://docs.microsoft.com/previous-versions/windows/desktop/cc904391(v=vs.85))バージョン2と[ndspi](network-direct-kernel-programming-interface--ndkpi-.md)の両方に適用されます。 使用される用語は次のとおりです。

-   ND は、NDSPI または NDK を参照するために使用されます。
-   *Nddisconnect*は、正常な切断を開始するために ND コンシューマーが行う関数呼び出しを参照するために使用されます。 NDSPI の場合、これは[**Indconnector::D isconnect**](https://docs.microsoft.com/previous-versions/windows/desktop/cc904364(v=vs.85))です。 NDKPI の場合は、 *Ndkdisconnect* ([*NDK\_FN\_DISCONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_disconnect)) になります。
-   *Nddisconnect を示す*値は、nd プロバイダーがピアからの正常な切断を受け取ったとき、または何らかの理由 (ローカル NDK 以外) によって接続が中止されたことを検出したときに、nd プロバイダーによって nd コンシューマーによって提供される指示を参照するために使用されます。独自の開始 ( *Nddisconnect*または*NdCloseConnector*の発行など)。

次に、A と B は ND 接続の両側を示しています。 コンシューマー A は側 A の ND コンシューマーを参照し、プロバイダー A は側 A の ND プロバイダーを参照します。同様のコンシューマー B/プロバイダー B は、B 側で同じエンティティを参照します。コンシューマー A が*Nddisconnect*を呼び出すと、プロバイダー a は、次の両方の条件が発生した場合にのみ、正常な切断通知をサイド B に送信し、コンシューマー a の*nddisconnect*要求を完了する必要があります。

-   次のいずれかを行います。
    -   B (コンシューマー A の*Nddisconnect*が正常に完了することにつながる) からの正常な切断通知を受信します。
    -   接続 abortion、タイムアウトなどのエラーが発生しました (コンシューマー A の*Nddisconnect*がエラーで完了するのを招きます)。
-   QP のすべての DMA アクティビティが完了しました (サイレント-成功フラグが付けられた作業要求の DMA アクティビティを含む)。

プロバイダー b がに対して正常な切断通知を受け取ったとき、または接続が中止されたことが検出されると、プロバイダー b が既に "プロバイダー B に*Nddisconnect* *を呼び出し*ました" というメッセージが表示されます。 着信の正常な切断通知または abort イベントは、ローカルコンシューマーが*Nddisconnect*を開始したときに発生する可能性があるため、ローカルコンシューマーは、ローカルコンシューマーの呼び出し *後に到着した nddisconnect 通知を処理するように準備する必要があります。NdDisconnect*。 *Ndno*の表示では、作業要求の完了に関して保証が提供されないことに注意してください。

切断された QP またはコネクタをコンシューマーが再利用することはできません。

NetworkDirect には、ハーフクローズ接続の概念がありません。 *Nddisconnect*が完了すると (成功または失敗)、接続は完全に閉じられます。

通常、コンシューマーは、発信側キューにポストされたすべての作業要求に対して入力候補を取得した後に、 *Nddisconnect*を呼び出す必要があります。 そうしないと、 *Nddisconnect*が真の正常な切断につながることはありません。 コンシューマーがそのような作業要求を未処理のままにする場合、プロバイダーは正常な切断をサポートする必要はありません。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






