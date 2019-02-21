---
title: NDIS 6.50 の概要
description: このセクションでは、NDIS 6.50 を紹介し、NDIS 6.40 からの変更について説明します。 Windows 10 バージョン 1507 以降では、NDIS 6.50 が含まれます。
ms.assetid: 8D2EA09D-3FA3-467B-861A-AA15C790FCD3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa3f2540e29fdca19a816387f37a5ed02ae781a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557833"
---
# <a name="introduction-to-ndis-650"></a>NDIS 6.50 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.50 を示し、その主要な設計の追加機能を説明します。 Windows 10 バージョン 1507 以降では、NDIS 6.50 が含まれます。

NDIS 6.50 は、NDIS 6.40 にマイナー バージョン更新です。 NDIS 6.50 する NDIS 6.x ドライバーの移植の詳細については、次を参照してください。 [NDIS 6.50 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-50.md)します。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.50 NDIS 6.40 を増分更新は、主要な新機能が含まれていません。

## <a name="implementing-an-ndis-650-driver"></a>NDIS 6.50、ドライバーを実装します。

NDIS 6.50、ドライバーがで定義されている要件に従う必要があります[、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.50、ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.50、ドライバーは、NDIS に登録する際に正しい NDIS バージョンをレポートする必要があります。
   
   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.50 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバーは 50 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[NDIS 6.50、ドライバーをコンパイルする](#compiling-an-ndis-650-driver))。

- Windows 10 用の NDIS 6.50 ミニポート ドライバー、バージョン 1507 以降は、データ構造の NDIS 6.50 バージョンを使用する必要があります。 詳細については、次を参照してください。[データ構造を使用する NDIS 6.50](#using-ndis-650-data-structures)します。

## <a name="compiling-an-ndis-650-driver"></a>NDIS 6.50、ドライバーのコンパイル

Windows 10 の WDK バージョン 1507 では、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.50 ドライバーがコンパイル時に適切な NDIS 6.50 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加```NDIS650_MINIPORT=1```します。
- フィルターまたはプロトコルのドライバーを追加```NDIS650=1```します。

Windows 10 バージョン 1507 リリース、WDK のドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。

## <a name="using-ndis-650-data-structures"></a>NDIS 6.50 データ構造を使用

### <a name="new-data-structures"></a>新しいデータの構造

次のデータ構造は、NDIS 6.50 の新機能。

- [OID_WWAN_SYS_CAPS](https://msdn.microsoft.com/library/windows/hardware/mt799833)
- [OID_WWAN_DEVICE_CAPS_EX](https://msdn.microsoft.com/library/windows/hardware/mt799830)
- [OID_WWAN_SLOT_INFO_STATUS](https://msdn.microsoft.com/library/windows/hardware/mt799832)
- [OID_WWAN_NETWORK_IDLE_HINT](https://msdn.microsoft.com/library/windows/hardware/dn931089) 
- [NDIS_STATUS_PD_CURRENT_CONFIG](https://msdn.microsoft.com/library/windows/hardware/dn931850)
- [NDIS_PD_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/dn931833)
- [NDIS_PD_CLOSE_PROVIDER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931834)
- [NDIS_PD_CONFIG](https://msdn.microsoft.com/library/windows/hardware/dn931835)
- [NDIS_PD_COUNTER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931836)
- [NDIS_PD_COUNTER_VALUE](https://msdn.microsoft.com/library/windows/hardware/dn931838)
- [NDIS_PD_FILTER_COUNTER](https://msdn.microsoft.com/library/windows/hardware/dn931839)
- [NDIS_PD_FILTER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931840)
- [NDIS_PD_ON_RSS_QUEUE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931841)
- [NDIS_PD_OPEN_PROVIDER_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931842)
- [NDIS_PD_PROVIDER_DISPATCH](https://msdn.microsoft.com/library/windows/hardware/dn931843)
- [NDIS_PD_QUEUE](https://msdn.microsoft.com/library/windows/hardware/dn931844)
- [NDIS_PD_QUEUE_DISPATCH](https://msdn.microsoft.com/library/windows/hardware/dn931845)
- [NDIS_PD_QUEUE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn931846)
- [NDIS_PD_RECEIVE_QUEUE_COUNTER](https://msdn.microsoft.com/library/windows/hardware/dn931848)
- [NDIS_PD_TRANSMIT_QUEUE_COUNTER](https://msdn.microsoft.com/library/windows/hardware/dn931849)
- [PD_BUFFER](https://msdn.microsoft.com/library/windows/hardware/dn931863)
- [PD_BUFFER_8021Q_INFO](https://msdn.microsoft.com/library/windows/hardware/dn931864)
- [PD_BUFFER_VIRTUAL_SUBNET_INFO](https://msdn.microsoft.com/library/windows/hardware/dn931865)

### <a name="updated-data-structures"></a>更新されたデータ構造体

次のデータ構造は、NDIS 6.50 で更新されました。

- [NET_PNP_EVENT_NOTIFICATION](https://msdn.microsoft.com/library/windows/hardware/ff568752)
- [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)
- [NDIS_NET_BUFFER_LIST_INFO](https://msdn.microsoft.com/library/windows/hardware/ff566569)
- [NdisMGetDeviceProperty](https://msdn.microsoft.com/library/windows/hardware/ff563592)
- [NDIS_SWITCH_OPTIONAL_HANDLERS](https://msdn.microsoft.com/library/windows/hardware/hh598219)
- [NDIS_SWITCH_NIC_SAVE_STATE](https://msdn.microsoft.com/library/windows/hardware/hh598216)

## <a name="ndis-651"></a>NDIS 6.51

NDIS 6.51 は、NDIS 6.50 に非常にマイナー バージョン更新です。 Windows 10 バージョン 1511 以降では、NDIS 6.51 が含まれます。 NDIS 6.50 のすべての情報にも適用されます NDIS 6.51 次の例外。

- MinorNdisVersion は、50 から 51 NDIS ドライバーに登録するときに変更します。
- コンパイラ設定を変更```NDIS650_MINIPORT=1```ミニポート ドライバーと```NDIS650=1```フィルターまたはプロトコルのドライバーを```NDIS651_MINIPORT=1```と```NDIS651=1```それぞれ。

