---
title: SR-IOV 機能の判断
description: SR-IOV 機能の判断
ms.assetid: 61895987-2469-471E-BB29-FF1CDD2869DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a4854dfe91ddaa4b8ee7995b7233abf2b4b0332
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381420"
---
# <a name="determining-sr-iov-capabilities"></a>SR-IOV 機能の判断


このトピックでは、NDIS とドライバーの後続のネットワーク アダプターのシングル ルート I/O 仮想化 (SR-IOV) 機能を特定する方法について説明します。 このトピックの内容は次のとおりです。

[レポートの中に、SR-IOV 機能*MiniportInitializeEx*](#reporting-sr-iov-capabilities-during-miniportinitializeex)

[上にあるドライバーが SR-IOV 機能の照会](#querying-sr-iov-capabilities-by-overlying-drivers)

## <a name="reporting-sr-iov-capabilities-during-miniportinitializeex"></a>レポートの中に、SR-IOV 機能*MiniportInitializeEx*


NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数の場合、ドライバーは、次の SR-IOV 機能を提供します。

-   ネットワーク アダプターをサポートできる、SR-IOV ハードウェア機能の完全なセット。

-   ネットワーク アダプターで現在有効になっている、SR-IOV 機能します。

-   かどうか、ミニポート ドライバーを管理、PCI Express (PCIe) 物理機能 (PF) 仮想機能 (VF) ネットワーク アダプターの。

ミニポート ドライバーを通じて基になるネットワーク アダプターの SR-IOV 対応のハードウェア機能の報告、 [ **NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)初期化されている構造体次のように

1. ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。

   NDIS 6.30 以降、ミニポート ドライバーの設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_SRIOV\_機能\_リビジョン\_1 と**サイズ**NDIS メンバー\_SIZEOF\_SRIOV\_機能\_リビジョン\_1。

2. ミニポート ドライバーでは、適切なフラグを設定、 **SriovCapabilities**レポート、SR-IOV 機能へのメンバー。

   ネットワーク アダプターでは、SR-IOV をサポートする場合の PCI Express (PCIe) 物理関数アダプターのミニポート ドライバーは、次のフラグを設定する必要があります。

   -   NDIS\_SRIOV\_CAP\_SRIOV\_サポートされています。

   -   NDIS\_SRIOV\_CAP\_PF\_ミニポート

   > [!NOTE]
   > PCIe 仮想機能 (VF) ネットワーク アダプターのミニポート ドライバーは、両方の NDIS を設定する必要があります\_SRIOV\_CAP\_VF\_ミニポート フラグは、NDIS\_SRIOV\_CAP\_SRIOV\_サポートされているフラグ。    

NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数の場合、ドライバーは次の手順に従って、ネットワーク アダプターの SR-IOV 機能に登録します。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

    ミニポート ドライバーのセット、 **HardwareSriovCapabilities**前に初期化されたへのポインターをメンバー [ **NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体。

    場合のレジストリ設定、  **\*SRIOV** INF キーワードは、1 つの値を持つ、SR-IOV 機能は、現在、ネットワーク アダプターで有効になっています。 ミニポート ドライバーのセット、 **CurrentSriovCapabilities**同じへのポインターをメンバー [ **NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体.

    場合のレジストリ設定、  **\*SRIOV** INF キーワードが 0 の値を持つ、ネットワーク アダプターの SR-IOV 機能は現在無効です。 ミニポート ドライバーを設定する必要があります、 **CurrentSriovCapabilities**メンバーを NULL にします。

    詳細については、  **\*SRIOV** INF キーワードを参照してください[SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

2.  ドライバー呼び出し[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)設定と、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

アダプターの初期化プロセスの詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

## <a name="querying-sr-iov-capabilities-by-overlying-drivers"></a>上にあるドライバーが SR-IOV 機能の照会


NDIS は次のように、ネットワーク アダプターにバインドされるドライバーに関連する、ネットワーク アダプターの現在有効になっている、SR-IOV 機能に渡します。

-   NDIS が上にあるフィルター ドライバーを呼び出すときに[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数、NDIS 通過ネットワーク アダプターの SR-IOV 機能、 *AttachParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体。 **SriovCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体。

-   NDIS が上位のプロトコル ドライバーを呼び出すときに[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数、NDIS 通過ネットワーク アダプターの SR-IOV 機能、 *BindParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体。 **SriovCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体。

NDIS も返されます、 [ **NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)のオブジェクト識別子 (OID) のクエリ要求を処理する場合に構造体[OID\_SRIOV\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-hardware-capabilities)と[OID\_SRIOV\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-current-capabilities)関連プロトコルによって発行されるか、ドライバーをフィルター処理します。

 

 





