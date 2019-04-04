---
title: SCSI ポートとの要求および解放デバイス要求のネゴシエート
description: SCSI ポートとの要求および解放デバイス要求のネゴシエート
ms.assetid: 0eb00955-127c-4ef7-a18f-69448b5fd105
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda2be72f5eed52d0a4e255e053a68d265f6f335
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570131"
---
# <a name="negotiating-claim-and-release-device-requests-with-scsi-port"></a>SCSI ポートとの要求および解放デバイス要求のネゴシエート


## <span id="ddk_negotiating_claim_and_release_device_requests_with_scsi_port_kg"></span><span id="DDK_NEGOTIATING_CLAIM_AND_RELEASE_DEVICE_REQUESTS_WITH_SCSI_PORT_KG"></span>


記憶域クラス ドライバーに SCSI ポートからのアクセス許可を要求する必要があります*要求*デバイス。 クラスのドライバーがデバイスを要求する方法の詳細については、[記憶域クラス ドライバー ClaimDevice ルーチン](storage-class-driver-s-claimdevice-routine.md)を参照してください。

新しいデバイスの検出および列挙のプロセスは、PnP デバイスや記憶域のプレ PnP デバイスいるかどうかによって異なります。 SCSI ポート ドライバー、同じデバイスを制御しようとする事前 PNP ドライバー パッケージと PnP ドライバー間を仲介します。 そのため、ストレージ デバイス ドライバーは、そのデバイスとやり取りする前に、SCSI ポートからアクセス許可を取得する必要があります。

デバイスを使用するためのアクセス許可を取得するデバイス ドライバーを要求に要求を送信 SCSI ポート、通常でその*AddDevice*ルーチン。 要求の要求が IRP の IOCTL の I/O 制御コードでは\_SCSI\_EXECUTE\_で、SRB へのポインターと NONE **Parameters.Scsi.Srb**します。 関数型 SRB では、SRB\_関数\_要求\_デバイス。

SCSI ポートは、各デバイス、デバイスが要求されているかどうかを示すフラグを保持します。 SCSI ポート、SRB への応答でこのフラグを設定する\_関数\_要求\_デバイス要求。SCSI ポート、SRB への応答にフラグをクリアする\_関数\_削除\_デバイス要求。

高度なドライバーが存在しないデバイスを要求しようとすると場合、SCSI ポートは IRP 要求の要求は失敗しのステータスを返します\_デバイス\_は\_いない\_が存在します。

高度なドライバーが既に要求されているデバイスを要求しようとすると場合、SCSI ポートは IRP 要求の要求は失敗し、状態のステータスを返します\_デバイス\_ビジーです。

要求の要求が成功すると、SCSI ポートは、SRB のデータ バッファーのポインターで、デバイスの現在のデバイス オブジェクトを返します。

以前に要求したデバイスを解放するより高度なドライバーは SCSI ポート ドライバーにリリース デバイス要求を送信する必要があります。リリースのデバイス要求、SRB とから成る、**関数**SRB の値\_関数\_リリース\_デバイス。

記憶域クラス ドライバーの観点からの要求のデバイス要求の詳細については、[記憶域クラス ドライバー ClaimDevice ルーチン](storage-class-driver-s-claimdevice-routine.md)を参照してください。

 

 




