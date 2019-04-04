---
title: SDP サーバーとの通信
description: SDP サーバーとの通信
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
ms.openlocfilehash: 374fec5c27b8f4beb594ebd914dd5d35ad096d02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578667"
---
# <a name="communicating-with-sdp-servers"></a>SDP サーバーとの通信


Bluetooth ドライバー スタックは、サービスの探索プロトコル (SDP) をサポートします。 このプロトコルでは、ローカルのオプションの範囲内にある Bluetooth デバイスによって提供されるサービスを検索または参照するプロファイルのドライバーを許可します。 SDP は、論理リンク コントロールと適応プロトコル (L2CAP)、トランスポート プロトコルとして使用し、クライアント/サーバー モデルに従います。

サービスは、情報、操作を実行または別のエンティティの代わりに、リソースを制御できるエンティティです。 サービスは、ソフトウェア、ハードウェア、またはハードウェアとソフトウェアの組み合わせとして実装する場合があります。 サービス レコードは、すべてのサービス属性の一覧で構成されます。

使用して、SDP プロトコルとそのサービスをアドバタイズできます L2CAP サーバー プロファイル ドライバー レジスタに自体を L2CAP 接続要求を受け入れるように後、 [ **IOCTL\_両方\_SDP\_送信\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff536693)または[ **IOCTL\_両方\_SDP\_送信\_レコード\_WITH\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536694)します。 各 SDP レコードは、ストリームとして送信されます。 プロファイルのドライバーは、IOCTL を使用している場合\_両方\_SDP\_送信\_レコード\_WITH\_については、プロファイルのドライバーの付加、 [**両方\_SDP\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff536650)生のストリームは、SDP の一部ではない追加の属性を格納する構造体自体を記録します。 これらには、要求元のクライアントのセキュリティ要件、SDP レコード、クラスからのデバイス (CoD) は、レコードおよびレコード自体の長さのパブリケーション オプションが含まれます。

プロファイルのドライバーはそのサービスをアドバタイズされた後、他の Bluetooth デバイスが検索またはこれらのサービスを参照できます。 SDP サービスの詳細については、[SDP サービスの情報へのアクセス](accessing-sdp-service-information.md)を参照してください。

プロファイルのドライバーが使用するには SDP をサービスのアドバタイズを停止するには、 [ **IOCTL\_両方\_SDP\_削除\_レコード**](https://msdn.microsoft.com/library/windows/hardware/ff536690)します。

 

 





