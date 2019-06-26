---
title: データ転送のキャンセル
description: データ転送のキャンセル
ms.assetid: a7900968-df57-41d9-abb1-4d2c97517362
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2565f99a249e30c3587a90080b1f99a654ac04dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366732"
---
# <a name="canceling-a-data-transfer"></a>データ転送のキャンセル





WIA アプリケーションと WIA ミニドライバーは、いつでも、データ転送をキャンセルすることができます。 WIA ミニドライバーがによって返される値をチェックして、アプリケーションがデータ転送を取り消すかどうかを判断することができます、 [ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)メソッド。 場合、メソッドが返す S\_false の場合、データ転送が取り消されました。 WIA ミニドライバーは、購入アクティビティをすべて停止する必要があります、アイドル状態に戻ります。 次のデータ転送の準備完了です。

WIA ミニドライバーを返すことによって、データ転送がキャンセルされたことを通知できます S\_から FALSE、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッド。 一部のデバイスでは、データ転送を中止できるハードウェア上で [キャンセル] ボタンがあります。 このような場合は、WIA ミニドライバーを返す必要があります S\_FALSE。

**注**  なし、エラーを宣言して、返す WIA スキャンでキャンセルすることは S\_FALSE。 ただし、Windows XP およびそれ以降のオペレーティング システムではのみWindows Millennium Edition ではありません。

 

コードから受信したすべての戻り値、 **IWiaMiniDrvCallBack::MiniDrvCallback**メソッドで返される、 **IWiaMiniDrv::drvAcquireItemData**メソッド。 アプリケーションで、エラー コードを返した場合、 **IWiaMiniDrvCallBack::MiniDrvCallback**メソッド、WIA ミニドライバー WIA サービスへのエラー コード、アイドル状態、および戻り値に戻り、データ転送は停止する必要があります。

 

 




