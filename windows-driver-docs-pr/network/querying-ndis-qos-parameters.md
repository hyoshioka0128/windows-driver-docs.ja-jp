---
title: NDIS QoS パラメーターのクエリ
description: NDIS QoS パラメーターのクエリ
ms.assetid: 875D39BA-D70D-4450-9F64-D08EAB54BDC2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 769406c8a8a83e80baf334ddd41c51d0397b2f35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844890"
---
# <a name="querying-ndis-qos-parameters"></a>NDIS QoS パラメーターのクエリ


プロトコルおよびフィルタードライバーは、次の方法でネットワークアダプターの NDIS Quality of Service (QoS) パラメーターを照会できます。

-   それまでのドライバーは、Oid のオブジェクト識別子 (OID) クエリ要求を使用して、操作の NDIS QoS パラメーターを照会できます。 [\_QoS\_操作\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)です。

-   これまでのドライバーは、oid [\_QoS\_リモート\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)を使用して、リモート NDIS QoS パラメーターを照会できます。

**注**  は、ローカルの NDIS QoS パラメーターを照会できません。

 

ローカル、リモート、および運用 NDIS の QoS パラメーターの詳細については、「 [Ndis Qos パラメーターの概要](overview-of-ndis-qos-parameters.md)」を参照してください。

NDIS はミニポートドライバーに対してこれらの OID 要求を処理し、要求された QoS パラメーターを[**ndis\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体内で返します。 NDIS は、次の方法でこれらの OID 要求を処理します。

-   NDIS は、Oid の oid クエリ要求を処理するときに、 [\_qos\_操作\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)を処理します。これは、以前の[**ndis\_ステータス\_qos\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)\_、ミニポートドライバーによって発行された変更の状態を示します。 このドライバーは、動作する QoS パラメーターが最初に解決されるか、後で変更されるときに、この状態を示します。

    ミニポートドライバーが Ndis\_の状態を発行する前に、それより前のドライバーが OID クエリ要求を発行すると[ **\_QOS\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)の状態を示す\_、ndis は、すべてのメンバー (**ヘッダー**メンバーを除く) を0に設定して、 [**ndis\_QOS PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を返します。

    また **、  ndis**は、ミニポートドライバーが ndis\_の状態を発行する場合にも、この構造を返します。 [**qos\_操作\_パラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change) 、 [**ndis\_Qos\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造 (**ヘッダー**メンバーを除く) が0に設定されています。\_

     

-   NDIS が oid クエリ要求を処理するときに、 [oid\_qos\_リモート\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)は、以前の[**ndis\_ステータス\_qos\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)からキャッシュされたリモート NDIS QOS パラメーターを返します。これは、ミニポートドライバーによって発行された\_変更の状態を示します。 ドライバーは、リモート QoS パラメーターが最初に解決されるか、後で変更されるときに、この状態を示します。

    ミニポートドライバーが[**ndis\_ステータス\_qos\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行する前に、そのドライバーが OID クエリ要求を発行した場合\_変更の状態を示す\_、ndis は、すべてのメンバー (**ヘッダー**メンバーを除く) を0に設定して、 [**ndis\_QOS PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体を返します。

    また **、  ndis**は、ミニポートドライバーが ndis\_の状態を発行する場合にも、この構造を返します。 [**qos\_操作\_パラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change) 、 [**ndis\_Qos\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造 (**ヘッダー**メンバーを除く) が0に設定されています。\_

     

 

 





