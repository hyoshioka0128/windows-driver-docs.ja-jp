---
title: Bluetooth IOCTL
description: Bluetooth IOCTL
ms.assetid: 384ea4bb-863c-4da7-bf81-85d2de734ef7
keywords:
- Bluetooth の WDK、Ioctl
- Ioctl WDK Bluetooth
- ローカル Bluetooth WDK
- リモートの Bluetooth WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ff7fdfc192e2b5c9897dbd562317484b996e48d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364654"
---
# <a name="bluetooth-ioctls"></a>Bluetooth IOCTL


Bluetooth ドライバー スタックに関する情報を収集するいくつかの Ioctl でプロファイルのドライバーを提供します。

-   ローカル Bluetooth 無線とシステム。

-   リモートの Bluetooth デバイス。

-   プラグ アンド プレイ (PnP) プロファイルのドライバーの読み込みにマネージャーの原因となったデバイス。

プロファイルのドライバーが使用するには、ローカルの Bluetooth 無線とシステムに関する情報を収集するには、 [ **IOCTL\_両方\_取得\_ローカル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)します。 IOCTL が返された後に、その**AssociatedIrp.SystemBuffer**メンバーにはへのポインターが含まれています、 [**両方\_ローカル\_ラジオ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ns-bthioctl-_bth_local_radio_info)、Bluetooth 無線のローカルとローカルの無線の検出し、に接続されているかどうかを示すフラグを含む、システムに関する情報を含む構造体。 返される両方\_ローカル\_ラジオ\_情報構造体が含まれています、[両方\_デバイス\_情報](https://go.microsoft.com/fwlink/p/?linkid=50713)構造体は、システムに固有の情報、および、が含まれています[**両方\_ラジオ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ns-bthioctl-_bth_radio_info)構造体は、ローカル オプションに固有の情報が含まれています。

プロファイルのドライバーが使用するには、特定のリモートの Bluetooth デバイスに関する情報を収集するには、 [ **IOCTL\_両方\_取得\_ラジオ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)します。 IOCTL が返された後に、その**AssociatedIrp.SystemBuffer**メンバーの両方へのポインターを格納する\_ラジオ\_特定のリモート オプションに関する情報を提供する情報の構造体かどうかなど、リモート ラジオの検出し、に接続されていることができます。

プロファイルのドライバーが使用するには検出されたすべてのリモート ラジオに関する情報を収集するには、 [ **IOCTL\_両方\_取得\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)します。 IOCTL が返された後に、その**AssociatedIrp.SystemBuffer**メンバーにはへのポインターが含まれています、 [**両方\_デバイス\_情報\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ns-bthioctl-_bth_device_info_list)両方の配列を含む構造体\_デバイス\_情報構造体。 両方の\_デバイス\_情報\_リスト構造がリモート無線を検出した各配列エントリが 1 つ含まれています。 ユーザー モード[BluetoothGetDeviceInfo](https://go.microsoft.com/fwlink/p/?linkid=74493) API はこの機能を使用して、すべてのリモート ラジオに関する情報を返します。

プロファイルのドライバーが使用するには、PnP マネージャー ファイルを読み込むことが原因となったリモート デバイスに関する情報を収集するには、 [ **IOCTL\_内部\_BTHENUM\_取得\_DEVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo). IOCTL が返された後に、その**AssociatedIrp.SystemBuffer**メンバーの両方へのポインターを格納する\_デバイス\_の Bluetooth デバイスを含め、リモート デバイスに関する情報を含む情報構造体アドレス、デバイスの状態、およびそのクラスのデバイス (CoD) 設定します。

プロファイルのドライバーを使用して[ **IOCTL\_内部\_BTHENUM\_取得\_ENUMINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo)基になるデバイスとサービスに関する情報を取得するにはPnP マネージャー プロファイルのドライバーの読み込みを原因となったとします。 IOCTL が返された後に、その**AssociatedIrp.SystemBuffer**メンバーにはへのポインターが含まれています、 [**両方\_列挙子\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_bth_enumerator_info)構造体ポート番号、デバイスのフラグ、仕入先 ID、および製品 ID など、デバイスに関するベンダー提供の情報を格納します。

Bluetooth の Ioctl および BRBs の使用に関する詳細については、次を参照してください。[のビルドと送信を BRB](building-and-sending-a-brb.md)します。

 

 





