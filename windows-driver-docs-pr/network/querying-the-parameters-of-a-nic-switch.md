---
title: NIC スイッチのパラメーターのクエリ
description: NIC スイッチのパラメーターのクエリ
ms.assetid: 8C1F0F8A-D290-4552-A324-062DB92F6B5D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8ebc8aab9f8bc57baf53403fae1713aefc98b0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844877"
---
# <a name="querying-the-parameters-of-a-nic-switch"></a>NIC スイッチのパラメーターのクエリ


このドライバーまたはユーザーアプリケーションは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターで作成された NIC スイッチのパラメーターを取得できます。 ドライバーまたはアプリケーションは、 [oid\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)のオブジェクト識別子 (oid) メソッドの要求を発行します。これらのパラメーターを取得するには、\_のパラメーターを\_します。

この OID メソッド要求を実行する前に、それまでのドライバーまたはユーザーアプリケーションが、 [ **\_PARAMETERS 構造\_スイッチの NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)を初期化する必要があります。 ドライバーまたはアプリケーションは、パラメーターが返される NIC スイッチの識別子に**Switchid**メンバーを設定する必要があります。

**注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。

 

この OID メソッド要求から正常に復帰した後、 [**ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)へのポインターが含まれ\_PARAMETERS 構造体がます. この構造体には、指定されたスイッチのパラメーターが含まれます。

NDIS は、ミニポートドライバーに対する[\_の\_スイッチ\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)要求の OID を処理します。 NDIS は、次のソースから、管理するデータの内部キャッシュから情報を返します。

-   レジストリ内の標準化された SR-IOV キーワード設定。 これらのキーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された INF キーワード」を参照してください。

-   Oid の OID 要求[\_nic\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)と[oid\_nic\_スイッチ\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)

 

 





