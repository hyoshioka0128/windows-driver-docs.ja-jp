---
title: NIC のスイッチ機能を判断します。
description: NIC のスイッチ機能を判断します。
ms.assetid: 5E627E52-2D47-4EA0-80D9-6979891CCE96
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990104d4b1d07ef6bdb8e1f4b3933c4316457bee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549460"
---
# <a name="determining-nic-switch-capabilities"></a>NIC のスイッチ機能を判断します。


このトピックでは、NDIS および上にあるドライバーを NIC はスイッチ シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの機能を特定する方法について説明します。 このトピックには、次の情報が含まれています。

[レポートの中に NIC のスイッチ機能*MiniportInitializeEx*](#report)

[上にあるドライバーによって NIC スイッチ機能の照会](#query)

**注**  専用の PCI Express (PCIe) 物理機能 (PF)、SR-IOV ネットワーク アダプターのミニポート ドライバーは、NIC のスイッチ機能を報告できます。 PCIe 仮想機能 (Vf) 用のミニポート ドライバーでは、NIC スイッチの SR-IOV 対応のアダプターの機能は報告する必要があります。

 

NIC のスイッチの詳細については、[NIC スイッチ](nic-switches.md)を参照してください。

## <a name="reporting-nic-switch-capabilities-during-miniportinitializeex"></a>レポートの中に NIC のスイッチ機能*MiniportInitializeEx*


NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の場合、ドライバーには、次の NIC はスイッチ機能。

-   NIC のハードウェア機能の完全なセットは、ネットワーク アダプターをサポートできることを切り替えます。

    **注**  NDIS 6.30 以降、1 つだけの NIC のスイッチを作成、ネットワーク アダプター。 このスイッチと呼ばれる、*既定 NIC スイッチ*します。

     

-   NIC は、ネットワーク アダプターで現在有効になっている機能を切り替えます。

ミニポート ドライバーを通じて基になるネットワーク アダプターの NIC スイッチ ハードウェア機能の報告、 [ **NDIS\_NIC\_切り替える\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)次のように初期化されている構造体。

1.  ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。

    NDIS 6.30 以降、ミニポート ドライバーの設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_NIC\_スイッチ\_機能\_リビジョン\_2 と**サイズ**NDIS メンバー\_SIZEOF\_NIC\_スイッチ\_機能\_リビジョン\_2。

2.  ミニポート ドライバーでは、適切なフラグを設定、 **NicSwitchCapabilities**のメンバー、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583) 、SR-IOV ネットワーク アダプターの NIC のスイッチ機能の構造体。 たとえば、ミニポート ドライバーは、NDIS を設定します\_NIC\_スイッチ\_CAP\_1 秒あたり\_VPORT\_INTERRUPT\_モデレート\_サポートされているフラグ NIC。スイッチは、各仮想ポート (VPort) スイッチで作成される割り込み節度をサポートしています。

3.  ミニポート ドライバーの設定の他のメンバー、 [ **NDIS\_NIC\_切り替える\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583) NIC のスイッチ機能の値の範囲の構造体SR-IOV ネットワーク アダプター。 たとえば、ミニポート ドライバーの設定、 **MaxNumVFs**と**MaxNumVPorts** Vf とアダプターをサポートする拡張の最大数をメンバー。

    **注**  ネットワーク アダプターで使用可能なハードウェア リソースに応じて、ミニポート ドライバーを設定できます、 **MaxNumVFs**メンバーである値をより小さい、  **\*NumVFs**キーワード。 このキーワードの詳細については、[SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)を参照してください。

     

NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の場合、ドライバーは次の手順に従って、ネットワーク アダプターの NIC のスイッチ機能に登録します。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

    ミニポート ドライバーのセット、 **HardwareNicSwitchCapabilities**前に初期化されたへのポインターをメンバー [ **NDIS\_NIC\_スイッチ\_機能** ](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。

    場合のレジストリ設定、  **\*SRIOV** INF キーワードは、1 つの値を持つ、ネットワーク アダプターが NIC スイッチの作成と構成の現在有効になります。 ミニポート ドライバーのセット、 **CurrentNicSwitchCapabilities**同じへのポインターをメンバー [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。

    場合のレジストリ設定、  **\*SRIOV** INF キーワードが 0 の値を持つ、NIC のスイッチの作成と構成のネットワーク アダプターが現在有効されません。 ミニポート ドライバーを設定する必要があります、 **CurrentNicSwitchCapabilities**メンバーを NULL にします。

    詳細については、  **\*SRIOV** INF キーワードを参照してください[SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

2.  ドライバー呼び出し[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)設定と、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

アダプターの初期化プロセスの詳細については、[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)を参照してください。

## <a name="querying-nic-switch-capabilities-by-overlying-drivers"></a>上にあるドライバーによって NIC スイッチ機能の照会


NDIS パス、ネットワーク アダプターの次のように、ネットワーク アダプターにバインドされるドライバーに関連する NIC のスイッチ機能が現在有効。

-   NDIS が上にあるフィルター ドライバーを呼び出すときに[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)関数、NDIS 渡しますネットワーク アダプターの NIC のスイッチ機能を通じて、 *AttachParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。 **NicSwitchCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。

-   NDIS が上位のプロトコル ドライバーを呼び出すときに[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数、NDIS 渡しますネットワーク アダプターの NIC のスイッチ機能を通じて、 *BindParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。 **NicSwitchCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。

NDIS も返されます、 [ **NDIS\_NIC\_スイッチ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)のオブジェクト識別子 (OID) のクエリ要求を処理する場合に構造体[OID\_NIC\_スイッチ\_ハードウェア\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569761)と[OID\_NIC\_スイッチ\_現在\_機能](https://msdn.microsoft.com/library/windows/hardware/ff569760)関連プロトコルまたはフィルター ドライバーによって発行されます。

 

 





