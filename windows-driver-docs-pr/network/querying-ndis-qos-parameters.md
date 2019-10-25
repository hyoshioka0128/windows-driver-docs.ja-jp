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

-   NDIS は、Oid の oid クエリ要求を処理するときに、 [\_qos\_操作\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)を処理します。これにより、前の\_ndis からキャッシュされた Operational ndis qos パラメーターが返され[ **\_qos\_operational が返されます。\_パラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change) 、ミニポートドライバーによって発行された状態の表示を変更します。 このドライバーは、動作する QoS パラメーターが最初に解決されるか、後で変更されるときに、この状態を示します。

    前のドライバーが OID クエリ要求を発行する前に、ミニポートドライバーが[**ndis の\_ステータス\_QOS\_操作\_パラメーター\_変更**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)の状態を示している場合、Ndis は[**ndis\_QOS を返し @no__** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)すべてのメンバーを含む T_10_ PARAMETERS 構造体 (**ヘッダー**メンバーを除く) が0に設定されています。

    また、 **ndis  、** ミニポートドライバーが[**NDIS\_の状態\_qos\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行し、ndis\_qos を使用して状態の表示を変更\_場合にも、この構造が返され[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)メンバー (**ヘッダー**メンバーを除く) が0に設定されているパラメーター構造体。

     

-   NDIS は、Oid の oid クエリ要求を処理するときに、[リモート\_のパラメーター\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)、以前の\_ndis からキャッシュされたリモートの ndis qos パラメーターを返します[**qos\_リモート\_パラメーター\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change) 、ミニポートドライバーによって発行された状態の表示を変更します。 ドライバーは、リモート QoS パラメーターが最初に解決されるか、後で変更されるときに、この状態を示します。

    前のドライバーが OID クエリ要求を発行する前に、ミニポートドライバーが[**ndis\_ステータス\_QOS\_リモート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)を発行して、状態の表示を変更\_、Ndis は[**ndis\_QOS を返し\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)すべてのメンバーを含むパラメーター構造 (**ヘッダー**メンバーを除く) が0に設定されます。

    また、 **ndis  、** ミニポートドライバーが[**NDIS\_の状態\_qos\_操作\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)を発行し、ndis\_qos を使用して状態の表示を変更\_場合にも、この構造が返され[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)メンバー (**ヘッダー**メンバーを除く) が0に設定されているパラメーター構造体。

     

 

 





