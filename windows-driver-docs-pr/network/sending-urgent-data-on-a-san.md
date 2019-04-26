---
title: SAN での緊急データの送信
description: SAN での緊急データの送信
ms.assetid: 9ff9719a-dd42-4ce7-8c07-370afa17fd7b
keywords:
- 緊急データ WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10370e2e6d1a6e44d6145abc9832ff5fa465f09f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346756"
---
# <a name="sending-urgent-data-on-a-san"></a>SAN での緊急データの送信





アプリケーションでは、SAN の緊急データを送信する場合、Windows Sockets は、データとしては、次の順序で説明されている転送を切り替えます。

1.  スイッチが受信要求の緊急データを送信する場合、 **WSPSend**を呼び出す、MSG\_OOB フラグを設定します。

2.  スイッチは、緊急のデータをコントロール メッセージ バッファーのペイロード部分にコピーします。

3.  スイッチは、適切なの SAN サービス プロバイダーを呼び出して[ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316) SAN ソケットでのリモート ピアの接続をコントロール メッセージに含まれている緊急のデータを送信する関数。 SAN NIC は、さらに、緊急データを送信します。

4.  リモート ピアにあるスイッチで、ポストされた受信バッファーに送信されるデータを受信する、 [ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)関数。

5.  リモート ピアにあるスイッチは、プライベート ストレージに、受信バッファーから受信したデータをコピーします。

6.  リモート ピアの呼び出しにあるスイッチ**WSPRecv**して受信バッファーを再送信します。

7.  リモート ピアにあるスイッチは、標準の Windows Sockets の手順に従って、アプリケーションにデータを提供します。

 

 





