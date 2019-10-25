---
title: Bluetooth IOCTL
description: Bluetooth IOCTL
ms.assetid: 384ea4bb-863c-4da7-bf81-85d2de734ef7
keywords:
- Bluetooth WDK、Ioctl
- Ioctl WDK Bluetooth
- ローカル Bluetooth WDK
- リモート Bluetooth WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8668dc295be7ea1470fc9da78d5e3176dce9986d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832138"
---
# <a name="bluetooth-ioctls"></a>Bluetooth IOCTL


Bluetooth ドライバースタックには、次の情報を収集するために、いくつかの Ioctl を持つプロファイルドライバーが用意されています。

-   ローカル Bluetooth ラジオとシステム。

-   リモート Bluetooth デバイス。

-   プラグアンドプレイ (PnP) マネージャーによってプロファイルドライバーが読み込まれる原因となったデバイス。

ローカル Bluetooth ラジオとシステムに関する情報を収集するために、プロファイルドライバーは[**IOCTL\_BTH\_使用して\_ローカル\_情報を取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)します。 IOCTL が返された後、その AssociatedIrp のメンバーには、ローカルの Bluetooth ラジオとシステムに関する情報を含む[**Bth\_ローカル\_RADIO\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_local_radio_info)構造体へのポインターが含まれてい**ます。** これには、ローカルラジオを検出して接続できるかどうかを示します。 返された BTH\_ローカル\_RADIO\_INFO 構造体には、システム固有の情報と[**bth\_RADIO\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_radio_info)構造体を含む[BTH\_デバイス\_info](https://go.microsoft.com/fwlink/p/?linkid=50713)構造体が含まれています。ローカルラジオ固有の情報が含まれています。

特定のリモート Bluetooth デバイスに関する情報を収集するために、プロファイルドライバーは[**IOCTL\_BTH\_GET\_ラジオ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)を使用します。 IOCTL が返された後、その AssociatedIrp のメンバーには、リモートラジオを検出できるかどうかなど、特定のリモートラジオに関する情報を提供する BTH\_RADIO\_INFO 構造体へのポインターが含まれてい**ます。** に接続しました。

検出されたすべてのリモートラジオに関する情報を収集するために、プロファイルドライバーは[**IOCTL\_BTH\_使用して\_デバイス\_情報を取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)します。 IOCTL が返された後、その**AssociatedIrp**のメンバーには、bth\_デバイス\_info 構造体の配列を含む[**BTH\_デバイス\_INFO\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ns-bthioctl-_bth_device_info_list)構造体へのポインターが含まれています。 BTH\_DEVICE\_INFO\_LIST 構造体には、検出された各リモートラジオの配列エントリが1つ含まれています。 ユーザーモードの[BluetoothGetDeviceInfo](https://go.microsoft.com/fwlink/p/?linkid=74493) API は、この機能を使用して、すべてのリモートラジオに関する情報を返します。

PnP マネージャーによって読み込まれる原因となったリモートデバイスに関する情報を収集するために、プロファイルドライバーは[**IOCTL\_内部\_BTHENUM\_\_DEVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)を使用します。 IOCTL が返された後、その AssociatedIrp のメンバーには、デバイスの Bluetooth デバイスのアドレス、デバイスの状態、その他のデバイスに関する情報を含む BTH\_デバイス\_情報構造体へのポインターが含まれてい**ます。** デバイスのクラス (CoD) 設定。

プロファイルドライバーは、 [**IOCTL\_内部\_BTHENUM\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo)を使用して\_ENUMINFO を取得し、基になるデバイスとサービスに関する情報を取得します。これにより、PnP マネージャーによるプロファイルドライバーの読み込みが発生します。 IOCTL が返された後、その AssociatedIrp のメンバーには、デバイスに関するベンダーから提供された情報を含む[**Bth\_列挙子\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_bth_enumerator_info)構造体へのポインターが含まれてい**ます。** これには、ポート番号、デバイスフラグ、ベンダー ID と製品 ID。

Bluetooth Ioctl および BRBs の使用方法の詳細については、「 [brbs の構築と送信](building-and-sending-a-brb.md)」を参照してください。

 

 





