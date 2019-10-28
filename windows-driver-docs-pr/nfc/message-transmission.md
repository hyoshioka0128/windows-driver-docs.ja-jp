---
title: メッセージの転送
description: メッセージの転送
ms.assetid: 96C5CE38-25EE-425A-A7C5-05990CBE2C3E
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 003d56f117aca0ab67bff31ef26653333d9e49f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843455"
---
# <a name="message-transmission"></a>メッセージの転送


NFP テクノロジによって、近接テクノロジで定義されているように、別のデバイスが近接されていると判断された場合、これはデバイス間で公開されたメッセージを送信するトリガーとして機能します。

発行されたメッセージは、デバイスが近接している間、1回だけ転送する必要があります。

現在公開されているすべてのメッセージは、デバイスが近接するたびに送信される必要があります。

デバイスが近接されている間にメッセージが公開され、トリガーがまだアクティブである場合、そのメッセージを送信する必要があります。

近接デバイスへのパブリケーションの配信は、そのパブリケーションが NFP プロバイダによって発行されていないという意味ではありません。 このパブリケーションは、クライアントが unpublishes するまで、次の近接イベントに対してアクティブなままになります。

NFP device driver インターフェイスでは、公開されたメッセージを、発行された順序で送信する必要はありません。 NFP デバイスドライバーインターフェイスでは、すべての公開メッセージを1つのブロックとして送信する必要はありません。 特に、NFC には、これを妨げる詳細な相互運用要件があります。1つのブロックとして複数のメッセージを送信することはできません。 ただし、個々の公開メッセージを完全に受信し、エラーが発生しないようにする必要があります。または、サブスクライブされたクライアントに渡すことはできません。

受信デバイス上のアプリがメッセージにサブスクライブされているかどうかをクライアントに通知するメカニズムは、NFP デバイスドライバーインターフェイスに定義されていません。 サブスクライブされていないメッセージが受信されたことをクライアントに通知するメカニズムもありません。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

