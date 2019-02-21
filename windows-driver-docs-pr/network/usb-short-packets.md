---
title: USB の短いパケット
description: USB の短いパケット
ms.assetid: e59476cf-754e-4550-849f-3aa645defe09
keywords:
- USB 短いパケット WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf6be1c082d5b96a25156a8f0e177e074cad94f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527238"
---
# <a name="usb-short-packets"></a>USB の短いパケット





USB は USB パケットは、混同しないで NDIS またはネットワーク パケットの形式でネットワーク経由でデータを渡します。 USB のパケットにまたは USB エンドポイントからの最大長の値に制限されます、 **wMaxPacketSize**のエンドポイントの記述子フィールド。 パイプの一括パケットの最大サイズは 64 バイトです。 特定の USB ホスト コント ローラーの制約がある短い USB パケット (たとえば、な少なく、64 バイト数は、ストリーミング データ) を使用してに関連付けられているペナルティがあります。

この制限を回避するリモート NDIS USB デバイスがゼロ バイトのパディングに追加データ メッセージようにする短いパケットは発生しません (の制約内で、 **MaxTransferSize**フィールド[リモート\_NDIS\_初期化\_MSG](remote-ndis-initialize-msg.md))。 **MessageLength**最後のフィールド[リモート\_NDIS\_パケット\_MSG](remote-ndis-packet-msg.md)追加これらを含まない埋め込みバイト。

デバイスが、最後の使用可能なリモートを転送する場合\_NDIS\_パケット\_MSG (されないように、デバイスのキューの詳細は残されます)、その短い USB パケットの送信を満たすものです。

場合、最後のリモート\_NDIS\_パケット\_(0 バイトの埋め込み) なしのデバイス送信リモート NDIS データ メッセージのメッセージは、長さが正確に USB パケットで終わる、 **wMaxPacketSize**をエンドポイントでは、後に、デバイス可能性がありますパケットを送信、その他の 1 バイト 0 転送の追加の一部として。 この許容量によっては、一部のデバイスの実装が簡略化します。

同様に、いくつかのデバイス側 USB チップセットが長さが USB パケットで終わる受信 USB 転送の終わりを検出しない、 **wMaxPacketSize**そのエンドポイントにします。 このため、ホストする必要があります 1 バイト 0 個のパケットに追加の倍数である長さがそれ以外の場合、データ転送、 **wMaxPacketSize**の受信側のエンドポイント。 リモートの NDIS の USB デバイスは、追加されたバイトを許容する必要があります。 **MessageLength**フィールドの最終的なリモコン\_NDIS\_パケット\_メッセージでは、この追加されたバイトは含まれません。

 

 





