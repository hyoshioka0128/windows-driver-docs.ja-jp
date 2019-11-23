---
title: Hyper-V 拡張可能スイッチの復元操作
description: Hyper-V 拡張可能スイッチの復元操作
ms.assetid: 283D9E43-79F2-47B1-8D29-39A8E7CBE2C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd0cc1665a2b10e8b90442db2b53e5e90ad1ce7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823837"
---
# <a name="hyper-v-extensible-switch-restore-operations"></a>Hyper-V 拡張可能スイッチの復元操作


Hyper-v の子パーティションが停止またはライブマイグレーションされた後に再起動されると、パーティションの実行時の状態が復元されます。 復元操作中、Hyper-v 拡張可能スイッチ拡張機能ドライバーは、拡張可能なスイッチネットワークアダプター (NIC) に関する実行時データを復元できます。

Hyper-v の子パーティションに対して復元操作を実行すると、拡張可能なスイッチインターフェイスは、拡張可能スイッチのプロトコルエッジに対して、 [oid\_スイッチ\_NIC\_の復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)に関する oid セット要求を発行するように通知します。 OID\_SWITCH\_NIC\_復元要求の**Informationbuffer**メンバーは、\_状態構造を保存するための[**ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)へのポインターを含んでいます。 [ **\_\_oid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)スイッチに対して、nic\_の構成を\_します。

この OID 要求を処理すると、拡張機能によって、ネットワークアダプターのランタイムデータが復元されます。 このランタイムデータは、以前 oid の oid 要求を使用して保存されています[\_スイッチ\_nic\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)と OID\_スイッチ\_NIC\_保存\_完了します。

[OID\_スイッチ\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)要求を受信すると、拡張可能なスイッチ拡張機能が実行時データを所有しているかどうかを最初に判断する必要があります。 このドライバーは、NDIS\_スイッチの**Extensionid**メンバーの値を比較することによってこれを行います[ **\_NIC\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造を、ドライバーが自身を識別するために使用する GUID 値に保存します。

拡張機能が実行時データを所有している場合は、次の方法でこのデータが復元されます。

1.  拡張機能は、 **SaveData**メンバーの実行時データをドライバーによって割り当てられたストレージにコピーします。

    **  ** NDIS\_スイッチの**ポート id**メンバーの値[ **\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造は、実行時データが保存された時点の**ポート id**値とは異なる場合があります。 これは、あるホストから別のホストへのライブマイグレーション中に実行時データが保存された場合に発生する可能性があります。 ただし、拡張可能スイッチ NIC の構成は、ライブマイグレーション中も保持されます。 これにより、拡張機能は、新しい**ポート id**値を使用して、実行時データを拡張可能スイッチ NIC に復元できます。

     

2.  拡張機能は、NDIS\_STATUS\_SUCCESS の OID set 要求を完了します。

拡張機能がランタイムデータを所有していない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す必要があります。 これにより、OID メソッド要求が拡張可能なスイッチドライバースタック内の基になる拡張機能に転送されます。 この手順の詳細については、「 [NDIS フィルタードライバーでの OID 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_スイッチ\_NIC\_復元\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)  
拡張可能スイッチのインターフェイスは、拡張可能スイッチのプロトコルエッジに対して、拡張可能スイッチの NIC の実行時データの復元操作の完了時にこの OID を発行するように通知します。

この OID 要求は、指定された拡張スイッチ NIC に対してのみ復元操作が完了したことを、拡張機能に通知します。

この OID 要求の詳細については、「 [oid\_SWITCH\_NIC\_復元\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)」を参照してください。

実行時データの復元操作では、拡張可能スイッチのプロトコルエッジによって oid の oid 要求が[\_切り替わり\_nic\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)および[oid\_スイッチ\_nic\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)\_hyper-v 子パーティションのネットワークインターフェイスの接続が完了します。 複数の Hyper-v 子パーティションが復元されると、プロトコルエッジによって個別の OID セットが発行されます。\_スイッチ\_NIC\_復元と OID\_切り替え\_NIC\_、各ネットワークインターフェイス接続に対する要求の完了を\_します。

拡張可能スイッチのプロトコルエッジでは、同じ NIC の実行時データの復元操作がインターリーブされない  に**注意**してください。 プロトコルエッジは、同じ NIC で前回の復元操作が完了した後にのみ、NIC に対して実行時のデータ復元操作を開始します。 ただし、別の NIC で別の復元操作が実行されている間に、プロトコルエッジが NIC の復元操作を開始する場合があります。 このため、拡張機能では非インターリーブ方式で復元操作を実行することを強くお勧めします。 たとえば、拡張機能では、別の nic に対して進行中の復元操作が完了する前に、別の NIC で新しい復元操作を開始できないと想定しないでください。

 

この OID 要求の詳細については、「 [Hyper-v 拡張可能スイッチの実行時データの復元](restoring-hyper-v-extensible-switch-run-time-data.md)」を参照してください。

 

 





