---
title: Hyper-V 拡張可能スイッチの保存操作
description: Hyper-V 拡張可能スイッチの保存操作
ms.assetid: 7148B094-2551-4035-A6BE-141DD01BEA14
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c92171a843685c950d157fe3472741fdd273a8a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823830"
---
# <a name="hyper-v-extensible-switch-save-operations"></a>Hyper-V 拡張可能スイッチの保存操作


Hyper-v の子パーティションが停止、保存、またはライブマイグレーションされると、パーティションの実行時の状態が保存されます。 保存操作中、Hyper-v 拡張可能スイッチ拡張機能は、拡張スイッチネットワークアダプター (NIC) に関する実行時データを保存できます。

Hyper-v 子パーティションで保存操作が実行されている場合、拡張可能スイッチインターフェイスは、操作について拡張機能に通知します。 拡張機能には、次のオブジェクト識別子 (OID) 要求を通じて通知されます。

<a href="" id="oid-switch-nic-save"></a>[OID\_スイッチ\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)  
拡張可能スイッチのインターフェイスは、拡張可能スイッチのプロトコルエッジに対して、拡張可能スイッチ NIC の保存操作中にこの OID を発行するように通知します。 この OID 要求を処理するときに、拡張機能は NIC のランタイムデータを返します。 実行時のデータが保存されると、 [oid\_スイッチ\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)の設定要求によって復元されます。

[OID\_スイッチ\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)メソッドの要求を受信すると、拡張機能は次のいずれかの操作を実行できます。

-   拡張機能に保存する実行時データがある場合は、 [**NDIS\_スイッチ\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)を初期化して\_状態構造を保存し、 **extensionid**メンバーなどのさまざまなメンバーを設定して保存するデータを識別します。 また、この拡張機能では、 **ndis\_スイッチ\_\_NIC**内のデータが保存されます。これにより、構造体の先頭から SaveDataOffset バイトが開始され\_状態構造が保存されます。その後、NDIS\_STATUS\_SUCCESS で OID メソッド要求を完了します。

-   [**Ndis\_スイッチ\_NIC\_SAVE\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体では、実行時の状態を保持するために十分なバッファーサイズが指定されていない場合、NDIS\_オブジェクト\_ヘッダー**サイズ**のメンバーで列挙されています。そのため、拡張機能は、メソッド構造体の*BYTESNEEDED*なフィールドを ndis\_\_に設定します。、およびは、NDIS\_STATUS\_BUFFER の OID を短時間\_\_に完了します。\_\_\_\_\_\_ OID は必要なサイズで再発行されます。
-   保存するランタイムデータが拡張機能にない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す必要があります。 これにより、OID メソッド要求が拡張可能なスイッチドライバースタック内の基になる拡張機能に転送されます。 この手順の詳細については、「 [NDIS フィルタードライバーでの OID 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。

この OID 要求の詳細については、「 [oid の処理\_スイッチ\_NIC\_保存要求](handling-the-oid-switch-nic-save-request.md)」を参照してください。

<a href="" id="oid-switch-nic-save-complete"></a>[OID\_\_NIC の切り替え\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)  
拡張可能スイッチのインターフェイスは、拡張可能スイッチのプロトコルエッジに対して、拡張可能スイッチの NIC の実行時データの保存操作の完了時にこの OID を発行するように通知します。

この OID 要求は、指定された拡張スイッチ NIC に対してのみ保存操作が完了したことを通知します。

この OID 要求の詳細については、次を参照してください。 [oid の処理\_スイッチ\_NIC\_保存\_要求を保存](handling-the-oid-switch-nic-save-complete-request.md)します。

実行時データの保存操作では、拡張可能スイッチのプロトコルエッジによって oid の oid 要求が\_されます。スイッチ[\_nic\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)および OID\_スイッチ\_NIC\_保存し、hyper-v の子パーティションのネットワークインターフェイスに対して\_を完了します。 複数の Hyper-v 子パーティションが停止またはライブマイグレーションされている場合は、プロトコルエッジによって個別の OID セットが発行されます。\_NIC\_保存および OID\_スイッチ\_\_、各ネットワークインターフェイス接続に対して完全な要求\_保存します。\_

拡張可能スイッチのプロトコルエッジでは、同じ NIC の実行時データに対して保存操作がインターリーブされない  に**注意**してください。 プロトコルエッジは、前回の保存操作が同じ NIC で完了した後にのみ、NIC に対して実行時のデータ保存操作を開始します。 ただし、別の NIC に対して別の保存操作が実行されている間に、プロトコルエッジが NIC に対して保存操作を開始する場合があります。 このため、拡張機能ではインターリーブなしの方法で保存操作を実行することを強くお勧めします。 たとえば、拡張機能では、別の nic に対して実行中の保存操作が完了する前に、別の NIC で新しい保存操作を開始できないことを想定しないでください。

 

 

 





