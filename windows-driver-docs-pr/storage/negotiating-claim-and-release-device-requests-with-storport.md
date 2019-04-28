---
title: Storport との要求および解放デバイス要求のネゴシエート
description: Storport との要求および解放デバイス要求のネゴシエート
ms.assetid: 9212f2b0-6319-47a6-8c61-02002ad81178
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fe5d55df4b7d5d70b0bd3b3f266494803c9439c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382742"
---
# <a name="negotiating-claim-and-release-device-requests-with-storport"></a>Storport との要求および解放デバイス要求のネゴシエート


記憶域クラス ドライバーが Storport にからアクセス許可を要求する必要があります*要求*デバイス。 クラスのドライバーがデバイスを要求する方法の詳細については、次を参照してください。[記憶域クラス ドライバー ClaimDevice ルーチン](storage-class-driver-s-claimdevice-routine.md)します。

新しいデバイスの検出および列挙のプロセスは、PnP デバイスや記憶域のプレ PnP デバイスいるかどうかによって異なります。 Storport ドライバー、同じデバイスを制御しようとする事前 PNP ドライバー パッケージと PnP ドライバー間を仲介します。 そのため、ストレージ デバイス ドライバーは、そのデバイスとやり取りする前に、Storport からアクセス許可を取得する必要があります。 さらに、対象のデバイスには、HBA 自体、または HBA で制御されるターゲットに接続されている LUN のいずれかがあります。 ストレージ クラス ドライバーによって要求されているデバイスの場合が、常に要求の LUN HBA ではありません。

デバイスを使用するアクセス許可を取得するには、デバイス ドライバーで Storport に要求の要求を送信します。 要求の要求が IRP の IOCTL の I/O 制御コードでは\_SCSI\_EXECUTE\_で、SRB へのポインターと NONE **Parameters.Scsi.Srb**します。 関数型 SRB では、SRB\_関数\_要求\_デバイス。

Storport では、各デバイス、デバイスが要求されているかどうかを示すフラグを保持します。 Storport、SRB への応答でこのフラグを設定する\_関数\_要求\_デバイス要求。Storport、SRB への応答にフラグをクリアする\_関数\_削除\_デバイス要求。

高度なドライバーが存在しないデバイスを要求しようとすると場合、Storport は IRP 要求の要求は失敗しのステータスを返します\_デバイス\_は\_いない\_が存在します。

高度なドライバーが既に要求されているデバイスを要求しようとすると場合、Storport は IRP 要求の要求は失敗し、状態のステータスを返します\_デバイス\_ビジーです。

要求の要求が成功すると、Storport、SRB のデータ バッファーのポインターで、デバイスの現在のデバイス オブジェクトを返します。

以前に要求したデバイスを解放するより高度なドライバーが Storport ドライバーをリリース デバイス要求を送信する必要があります。リリースのデバイス要求、SRB とから成る、**関数**SRB の値\_関数\_リリース\_デバイス。

記憶域クラス ドライバーの観点からの要求のデバイス要求の詳細については、次を参照してください。[記憶域クラス ドライバー ClaimDevice ルーチン](storage-class-driver-s-claimdevice-routine.md)します。

 

 




