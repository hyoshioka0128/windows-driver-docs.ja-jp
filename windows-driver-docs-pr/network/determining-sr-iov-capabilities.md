---
title: SR-IOV 機能の判断
description: SR-IOV 機能の判断
ms.assetid: 61895987-2469-471E-BB29-FF1CDD2869DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95b2302470e0795960a1525450dffe4df205c07e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834907"
---
# <a name="determining-sr-iov-capabilities"></a>SR-IOV 機能の判断


このトピックでは、NDIS およびそれ以降のドライバーがネットワークアダプターのシングルルート i/o 仮想化 (SR-IOV) 機能をどのように決定するかについて説明します。 このトピックの内容は次のとおりです。

[*MiniportInitializeEx*中の sr-iov 機能の報告](#reporting-sr-iov-capabilities-during-miniportinitializeex)

[それまでのドライバーによる SR-IOV 機能のクエリ](#querying-sr-iov-capabilities-by-overlying-drivers)

## <a name="reporting-sr-iov-capabilities-during-miniportinitializeex"></a>*MiniportInitializeEx*中の sr-iov 機能の報告


NDIS がミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ドライバーは次の sr-iov 機能を提供します。

-   ネットワークアダプターがサポートできる SR-IOV ハードウェア機能の完全なセット。

-   ネットワークアダプターで現在有効になっている SR-IOV 機能。

-   ミニポートドライバーが、ネットワークアダプター上の PCI Express (PCIe) 物理機能 (PF) または仮想機能 (VF) を管理しているかどうか。

ミニポートドライバーは、次の方法で初期化される[**NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)の構造を通じて、基になるネットワークアダプターの sr-iov ハードウェア機能を報告します。

1. ミニポートドライバーは、**ヘッダー**メンバーを初期化します。 ドライバーは、**ヘッダー**の**type**メンバーを、既定\_\_型の NDIS\_OBJECT に設定します。

   NDIS 6.30 以降では、ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_SRIOV\_機能 \_リビジョン\_1、 **SIZE**メンバーを NDIS\_SIZEOF\_SRIOV\_機能\_リビジョン\_1 に設定します。

2. このミニポートドライバーは、SR-IOV 機能を報告するために**Sriの機能**メンバーに適切なフラグを設定します。

   ネットワークアダプターが sr-iov をサポートしている場合、アダプターの PCI Express (PCIe) 物理機能のミニポートドライバーでは、次のフラグを設定する必要があります。

   -   NDIS\_SRIOV\_CAPS\_SRIOV\_サポートされています

   -   NDIS\_SRIOV\_CAP\_PF\_ミニポート

   > [!NOTE]
   >ネットワークアダプターの PCIe 仮想機能 (VF) のミニポートドライバー  、NDIS\_SRIOV\_CAPS\_VF\_ミニポートフラグと NDIS\_SRIOV\_CAPS\_SRIOV\_supported フラグの両方を設定する必要があります。    

NDIS がミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ドライバーは次の手順に従ってネットワークアダプターの sr-iov 機能を登録します。

1.  ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造を初期化します。

    ミニポートドライバーは、以前に初期化された[**NDIS\_SRIOV\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体へのポインターに、**ハード waresriricapabilities**メンバーを設定します。

    **\*SRIOV** INF キーワードのレジストリ設定の値が1である場合、sr-iov 機能はネットワークアダプターで現在有効になっています。 ミニポートドライバーは、 **CurrentsriSRIOV**機能のメンバーを、同じ[**NDIS\_\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体へのポインターに設定します。

    **\*SRIOV** INF キーワードのレジストリ設定の値が0の場合、sr-iov 機能はネットワークアダプターで現在無効になっています。 ミニポートドライバーでは、 **Currentsriの機能**メンバーを NULL に設定する必要があります。

    **\*SRIOV** INF キーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された inf キーワード」を参照してください。

2.  ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、 *miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

アダプター初期化プロセスの詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

## <a name="querying-sr-iov-capabilities-by-overlying-drivers"></a>それまでのドライバーによる SR-IOV 機能のクエリ


NDIS は、ネットワークアダプターの現在有効な SR-IOV 機能を、次の方法でネットワークアダプターにバインドするドライバーに渡します。

-   NDIS が後続のフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出すと、Ndis は*attachparameters*パラメーターを使用して、ネットワークアダプターの sr-iov 機能を渡します。 このパラメーターには、\_PARAMETERS 構造体を[**アタッチ\_ための NDIS\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)へのポインターが含まれています。 この構造体の**SriSRIOV capabilities**メンバーには、 [**NDIS\_\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体へのポインターが含まれています。

-   NDIS が、プロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、Ndis は*bindparameters*パラメーターを使用してネットワークアダプターの sr-iov 機能を渡します。 このパラメーターには、\_PARAMETERS 構造体を[**アタッチ\_ための NDIS\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)へのポインターが含まれています。 この構造体の**SriSRIOV capabilities**メンバーには、 [**NDIS\_\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体へのポインターが含まれています。

また、NDIS は、 [SRIOV\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-hardware-capabilities)および oid\_のオブジェクト識別子 (oid) クエリ要求を処理するときに、 [**ndis\_SRIOV\_capabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体を返します。これは、プロトコルまたはフィルタードライバーによって発行される[現在の\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-current-capabilities)です。\_\_

 

 





