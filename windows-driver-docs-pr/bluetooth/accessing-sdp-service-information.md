---
title: SDP サービス情報へのアクセス
description: SDP サービス情報へのアクセス
ms.assetid: 0b327fbd-1101-4566-ac2f-3d039eed6835
keywords:
- Bluetooth WDK、SDP サーバー通信
- SDP WDK Bluetooth
- サービス検出プロトコル WDK Bluetooth
- サービスの参照 (WDK) Bluetooth
- サービスの検索 WDK Bluetooth
- サービス閲覧 WDK Bluetooth
- IOCTL_BTH_SDP_CONNECT
- SDP レコードの検索 WDK Bluetooth
- IOCTL_BTH_SDP_SERVICE_SEARCH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba84a61be48ad4af19f514fd20cb4ca722805f03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833877"
---
# <a name="accessing-sdp-service-information"></a>SDP サービス情報へのアクセス


プロファイルドライバーが sdp を使用してサービスを提供するためにサービス検出プロトコル (SDP) レコードを送信すると、他のデバイスはそのレコードを検索するか、検索することによって、これらのサービスを検出できます。

SDP レコードを検索するには、クライアントプロファイルドライバーはまず[**IOCTL\_BTH\_sdp\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)を使用して、リモートデバイスの sdp サービスに接続する必要があります。

プロファイルドライバーは、次のいずれかの Ioctl を使用して、実際の SDP レコード検索を実行できます。

-   [**IOCTL\_BTH\_sdp\_属性\_検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)では、指定された sdp 属性範囲に含まれるリモート SDP レコードのすべてのコンポーネントを取得します。

-   [**IOCTL\_BTH\_sdp\_サービス\_検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)では、リモートデバイスに sdp 要求を発行し、特定のサービスクラスまたはクラスの sdp レコードへのハンドルを要求します。

-   [**Ioctl\_bth\_sdp\_サービス\_属性\_検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)では、ioctl\_BTH\_SDP\_属性\_、検索と ioctl\_BTH\_SDP\_SERVICE が結合され\_属性\_検索を実行し、1回の操作で使用可能な SDP レコードストリームを返します。

プロファイルドライバーは、IOCTL\_BTH\_SDP\_サービス\_検索および IOCTL\_の SDP\_属性\_検索を使用して、Bluetooth リンクを介して送信される SDP トラフィックの量を減らし、最大転送単位 (Mtu) を少なくすることによって必要な情報を指定します。 これらの問題がどちらも問題にならない場合は、プロファイルドライバーが IOCTL\_BTH\_SDP\_サービス\_属性\_検索を呼び出すと便利です。

プロファイルドライバーは、目的のサービスの*動的*プロトコル/サービスマルチプレクサー (PSM) を取得した後、 **BRB\_L2CA\_OPEN\_CHANNEL** brb を使用してリモートサービスに接続できます。

**注**  サービスに固定 psm がある場合、多くの場合、L2CAP クライアントプロファイルドライバーは SDP を使用して psm を取得する必要がありません。 ただし、L2CAP クライアントプロファイルドライバーでは、sdp を使用して SDP サーバーの属性を取得することもできます。

 

プロファイルドライバーが検索を終了したら、 [**IOCTL\_BTH\_SDP\_disconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)を使用して、リモート sdp サーバーから切断します。

 

 





