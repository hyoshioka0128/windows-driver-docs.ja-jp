---
title: データ転送のキャンセル
description: データ転送のキャンセル
ms.assetid: a7900968-df57-41d9-abb1-4d2c97517362
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0ffdf121fb9e80b3e148aea92866a096ef2e95a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840883"
---
# <a name="canceling-a-data-transfer"></a>データ転送のキャンセル





WIA アプリケーションと WIA ミニドライバーは、いつでもデータ転送をキャンセルできます。 WIA ミニドライバーは、 [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)メソッドによって返された値をチェックすることによって、アプリケーションでデータ転送が取り消されたかどうかを判断できます。 メソッドからが返された場合、\_FALSE の場合、データ転送は取り消されています。 WIA ミニドライバーは、すべての取得アクティビティを停止し、アイドル状態に戻す必要があります。 その後、次のデータ転送の準備が整います。

WIA ミニドライバーは、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドから S\_FALSE を返すことによって、データ転送が取り消されたことを通知できます。 一部のデバイスには、データ転送を中止できるハードウェア上の [キャンセル] ボタンがあります。 このような場合、WIA ミニドライバーは\_FALSE を返す必要があります。

  、エラーを宣言して、S\_FALSE を返すことなく、WIA スキャンをキャンセルできることに**注意**してください。 ただし、これは Windows XP 以降のオペレーティングシステムでのみ可能です。Windows Millennium Edition では使用できません。

 

**IWiaMiniDrvCallBack:: MiniDrvCallback**メソッドから受け取ったすべてのリターンコードは、 **IWiaMiniDrv::d rvacquireitemdata**メソッドで返される必要があります。 アプリケーションから**IWiaMiniDrvCallBack:: MiniDrvCallback**メソッドでエラーコードが返された場合、wia ミニドライバーはデータ転送を停止し、アイドル状態に戻り、そのエラーコードを wia サービスに返す必要があります。

 

 




