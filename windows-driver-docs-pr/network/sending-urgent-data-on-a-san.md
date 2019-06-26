---
title: SAN での緊急データの送信
description: SAN での緊急データの送信
ms.assetid: 9ff9719a-dd42-4ce7-8c07-370afa17fd7b
keywords:
- 緊急データ WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2168866c5b17ec8deb1b15c72d0c896646ff055a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386833"
---
# <a name="sending-urgent-data-on-a-san"></a>SAN での緊急データの送信





アプリケーションでは、SAN の緊急データを送信する場合、Windows Sockets は、データとしては、次の順序で説明されている転送を切り替えます。

1.  スイッチが受信要求の緊急データを送信する場合、 **WSPSend**を呼び出す、MSG\_OOB フラグを設定します。

2.  スイッチは、緊急のデータをコントロール メッセージ バッファーのペイロード部分にコピーします。

3.  スイッチは、適切なの SAN サービス プロバイダーを呼び出して[ **WSPSend** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85)) SAN ソケットでのリモート ピアの接続をコントロール メッセージに含まれている緊急のデータを送信する関数。 SAN NIC は、さらに、緊急データを送信します。

4.  リモート ピアにあるスイッチで、ポストされた受信バッファーに送信されるデータを受信する、 [ **WSPRecv** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85))関数。

5.  リモート ピアにあるスイッチは、プライベート ストレージに、受信バッファーから受信したデータをコピーします。

6.  リモート ピアの呼び出しにあるスイッチ**WSPRecv**して受信バッファーを再送信します。

7.  リモート ピアにあるスイッチは、標準の Windows Sockets の手順に従って、アプリケーションにデータを提供します。

 

 





