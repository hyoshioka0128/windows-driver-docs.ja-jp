---
title: SDP サーバーとの通信の概要
description: SDP サーバーとの通信の概要
ms.assetid: 833f2eea-d7e6-4f19-979e-3bb4db47fa43
keywords:
- Bluetooth WDK、SDP サーバー通信
- SDP WDK Bluetooth
- サービス検出プロトコル WDK Bluetooth
- プロファイル ドライバー WDK Bluetooth
- サービスの参照 (WDK) Bluetooth
- サービスの検索 WDK Bluetooth
- サービス閲覧 WDK Bluetooth
- アドバタイズサービス WDK Bluetooth
- WDK Bluetooth を提供するサービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73e2acf2f525ea25bd849ca2500ff6a1988280f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832121"
---
# <a name="communicating-with-sdp-servers-overview"></a>SDP サーバーとの通信の概要


Bluetooth ドライバースタックでは、サービス検出プロトコル (SDP) がサポートされています。 このプロトコルを使用すると、プロファイルドライバーは、ローカルラジオの範囲内にある Bluetooth デバイスによって提供されるサービスを検索または参照することができます。 SDP は、そのトランスポートプロトコルとして論理リンク制御とアダプテーションプロトコル (L2CAP) を使用し、クライアント/サーバーモデルに従います。

サービスは、情報の提供、アクションの実行、または別のエンティティの代わりにリソースの制御を行うことができる任意のエンティティです。 本サービスは、ソフトウェア、ハードウェア、またはハードウェアとソフトウェアの組み合わせとして実装される場合があります。 サービスレコードは、サービス属性の一覧で構成されます。

L2CAP server プロファイルドライバーは、着信 L2CAP 接続要求を受け入れるように自身を登録した後、 [**IOCTL\_BTH\_sdp\_送信\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)または ioctl を使用して、そのサービスを sdp プロトコルでアドバタイズでき[ **\_BTH\_SDP\_\_レコード\_を\_情報と共に送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)します。 各 SDP レコードは、ストリームとして送信されます。 プロファイルドライバーが IOCTL を使用して\_BTH\_SDP\_\_情報と共に\_レコード\_を送信する場合、プロファイルドライバーは[**Bth\_SDP\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_sdp_record)構造の前に生のストリームを付加します。 SDP レコード自体に含まれていない追加の属性が含まれています。 これには、要求元のクライアントのセキュリティ要件、SDP レコードのパブリケーションオプション、デバイスのクラス (CoD) 情報、レコードの長さ、レコード自体が含まれます。

プロファイルドライバーがサービスを提供した後、他の Bluetooth デバイスがこれらのサービスを検索または参照できるようになります。 SDP サービスの詳細については、「 [Sdp サービス情報へのアクセス](accessing-sdp-service-information.md)」を参照してください。

SDP でサービスのアドバタイズを停止するには、プロファイルドライバーが[**IOCTL\_BTH\_sdp\_\_レコードを削除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)します。

 

 





