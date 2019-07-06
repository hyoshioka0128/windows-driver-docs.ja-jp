---
title: SDP サーバーの概要との通信
description: SDP サーバーの概要との通信
ms.assetid: 833f2eea-d7e6-4f19-979e-3bb4db47fa43
keywords:
- Bluetooth の WDK、SDP サーバー間の通信
- SDP WDK Bluetooth
- サービス探索プロトコルの WDK Bluetooth
- プロファイル ドライバー WDK Bluetooth
- WDK Bluetooth サービスを参照
- WDK Bluetooth サービスを検索
- WDK の Bluetooth の参照サービス
- WDK の Bluetooth の広告サービス
- WDK の Bluetooth の広告サービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40c08eb94e5f354f13533b875a2f3f5bf9326d56
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608470"
---
# <a name="communicating-with-sdp-servers-overview"></a>SDP サーバーの概要との通信


Bluetooth ドライバー スタックは、サービスの探索プロトコル (SDP) をサポートします。 このプロトコルでは、ローカルのオプションの範囲内にある Bluetooth デバイスによって提供されるサービスを検索または参照するプロファイルのドライバーを許可します。 SDP は、論理リンク コントロールと適応プロトコル (L2CAP)、トランスポート プロトコルとして使用し、クライアント/サーバー モデルに従います。

サービスは、情報、操作を実行または別のエンティティの代わりに、リソースを制御できるエンティティです。 サービスは、ソフトウェア、ハードウェア、またはハードウェアとソフトウェアの組み合わせとして実装する場合があります。 サービス レコードは、すべてのサービス属性の一覧で構成されます。

使用して、SDP プロトコルとそのサービスをアドバタイズできます L2CAP サーバー プロファイル ドライバー レジスタに自体を L2CAP 接続要求を受け入れるように後、 [ **IOCTL\_両方\_SDP\_送信\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)または[ **IOCTL\_両方\_SDP\_送信\_レコード\_WITH\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)します。 各 SDP レコードは、ストリームとして送信されます。 プロファイルのドライバーは、IOCTL を使用している場合\_両方\_SDP\_送信\_レコード\_WITH\_については、プロファイルのドライバーの付加、 [**両方\_SDP\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ns-bthioctl-_bth_sdp_record)生のストリームは、SDP の一部ではない追加の属性を格納する構造体自体を記録します。 これらには、要求元のクライアントのセキュリティ要件、SDP レコード、クラスからのデバイス (CoD) は、レコードおよびレコード自体の長さのパブリケーション オプションが含まれます。

プロファイルのドライバーはそのサービスをアドバタイズされた後、他の Bluetooth デバイスが検索またはこれらのサービスを参照できます。 SDP サービスの詳細については、次を参照してください。 [SDP サービスの情報へのアクセス](accessing-sdp-service-information.md)します。

プロファイルのドライバーが使用するには SDP をサービスのアドバタイズを停止するには、 [ **IOCTL\_両方\_SDP\_削除\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)します。

 

 





