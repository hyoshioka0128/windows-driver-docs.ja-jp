---
title: ネットワーク アダプターでの NIC スイッチの列挙
description: ネットワーク アダプターでの NIC スイッチの列挙
ms.assetid: 0799A879-2BC0-43C5-A6B6-6D46C74A26FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b3f233238d95730000afffa430f0085dfd835c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838119"
---
# <a name="enumerating-nic-switches-on-a-network-adapter"></a>ネットワーク アダプターでの NIC スイッチの列挙


このドライバーまたはユーザーアプリケーションは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターで作成されたすべての NIC スイッチの一覧を取得できます。 ドライバーまたはアプリケーションは、Oid\_NIC のオブジェクト識別子 (OID) クエリ要求を発行します。この一覧を取得するには、 [ENUM\_スイッチ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)スイッチを\_します。

この OID 要求から正常に戻った後、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、次の情報を含むバッファーへのポインターが含まれています。

-   [**NDIS\_NIC\_スイッチ\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)内の要素の数を定義する配列構造体です。

-   \_情報構造体の[**NDIS\_NIC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)の配列。 これらの各構造体には、ネットワークアダプターで作成された1つの NIC スイッチに関する情報が含まれています。

    **注**  ネットワークアダプターに nic スイッチがない場合、ドライバーは、NDIS\_Nic の**numelements**メンバー [ **\_スイッチ\_情報\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)構造を0に設定し、 [**ndis\_NIC を設定しません\_スイッチ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)構造体が返されます。

     

**注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。

 

NDIS は、ミニポートドライバーの\_列挙\_スイッチ要求を使用して、 [OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)を処理します。 NDIS は、次のソースから、管理するデータの内部キャッシュから情報を返します。

-   レジストリ内の標準化された SR-IOV キーワード設定。 これらのキーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された INF キーワード」を参照してください。

-   Oid の OID 要求[\_nic\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)と[oid\_nic\_スイッチ\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)

**  ndis**では、Ndis の**NicSwitchArray**メンバーに含まれるスイッチの列挙も提供されています。 [ **\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)と[**ndis\_FILTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)をバインドして\_パラメーターをアタッチ\_ます。構成. そのため、それ以降のプロトコルとフィルタードライバーでは、 [OID\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)を発行する必要はありません。\_列挙\_は、この情報を取得するための要求をスイッチ\_ます。

 

 

 





