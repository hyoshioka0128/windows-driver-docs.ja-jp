---
title: デバイス固有のコンテキスト
description: デバイス固有のコンテキスト
ms.assetid: 29e0d451-57fb-4943-9508-022adffa4650
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58734bfa92a525b24448ace9a00f738ce7645537
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385933"
---
# <a name="device-specific-contexts"></a>デバイス固有のコンテキスト





ミニドライバーと必要に応じて、デバイスに固有の情報を格納するためのプライベート コンテキストを使用します。 このデバイスに固有のコンテキストでは、時間、ミニドライバーがデバイスの情報を取得するデバイスを呼び出す必要がありますの数を減らすことができます。 特定のミニドライバーのドライバーの項目ごとに 1 つだけのデバイス固有のコンテキストがあります。 ドライバーの項目が不要、WIA サービス呼び出しミニドライバーの[ **IWiaMiniDrv::drvFreeDrvItemContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)すべてのデバイスに固有にアタッチされているリソースを解放しますコンテキスト。

たとえば、カメラ ドライバーは、デバイスからサムネイルのデータを取得するとき、通常はキャッシュ適切なドライバーの項目に関連付けられているドライバーのコンテキストでのデータします。 WIA サービスが、コンテキストを解放することに注意してください。 ドライバーの責任では、そのコンテキストによって保持されているすべてのリソースを解放することです。 場合は、前の例のサムネイルのデータが格納されたデバイスに固有のコンテキストで割り当てられたメモリのキャッシュされたデータをメモリ保持しているがコンテキスト自体ではありませんが、ここでは、解放必要があります。

 

 




