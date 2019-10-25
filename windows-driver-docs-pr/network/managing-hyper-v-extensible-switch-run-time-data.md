---
title: Hyper-V 拡張可能スイッチ実行時データの管理
description: Hyper-V 拡張可能スイッチ実行時データの管理
ms.assetid: 08A353F5-D8CB-4645-9337-8169D302F6F2
ms.date: 12/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: b52fdc73bcaeb16b2ddd51296d5a18d3a9c6de70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844119"
---
# <a name="managing-hyper-v-extensible-switch-run-time-data"></a>Hyper-V 拡張可能スイッチ実行時データの管理

このトピックでは、Hyper-v 拡張可能スイッチ拡張機能の保存と復元の操作について説明します。 これらの操作により、拡張機能は、拡張可能な個々のスイッチネットワークアダプター (Nic) の実行時データを保存および復元できます。 これらの操作は、拡張可能なスイッチポートへのネットワークアダプター接続がある Hyper-v 子パーティションが停止または開始されているときに実行されます。

## <a name="saving-hyper-v-extensible-switch-run-time-data"></a>Hyper-v 拡張可能スイッチの実行時データを保存しています

このセクションでは、Hyper-v 拡張可能スイッチ拡張機能を使用して個々のネットワークアダプター (Nic) の実行時データを保存する操作について説明します。 この操作は、拡張可能なスイッチポートへのネットワークアダプター接続がある Hyper-v 子パーティションが停止されているか、その状態が保存されているときに実行されます。

### <a name="handling-the-oid_switch_nic_save-request"></a>OID\_スイッチ\_NIC\_保存要求

拡張可能なスイッチポートへのネットワークアダプター接続がある Hyper-v 子パーティションが停止されるか、その状態が保存されると、Hyper-v 拡張可能スイッチインターフェイスが通知されます。 これにより、拡張可能スイッチのプロトコルエッジで、Oid のオブジェクト識別子 (OID) メソッド要求が発行され、 [\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)が拡張可能なスイッチドライバースタック\_保存されます。 拡張可能なスイッチ拡張機能がこの OID 要求を受け取ると、子パーティションにアタッチされている、指定されたネットワークアダプター接続の実行時データを保存できます。

[Oid\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)の[ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**INFORMATIONBUFFER**メンバーには、nic の\_の\_スイッチへのポインターが含まれています。 [ **\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造を保存します。 この構造体は、拡張可能なスイッチのプロトコルエッジによって割り当てられ、次のように初期化されます。

-   **ヘッダー**メンバーは、現在の型を含むように初期化されます。 [ **\_、NDIS スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造です。 サイズは、完全なバッファーサイズに設定されます。

-   **ポート id**メンバーには、保存操作を実行する拡張可能なスイッチポートの一意の識別子が含まれています。

[OID\_スイッチ\_NIC\_SAVE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)メソッド要求を受信すると、次のように拡張機能が実行されます。

1.  拡張機能は、 [**NDIS\_スイッチ\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)の**ポート id**メンバーを読み取り、\_状態の構造を保存\_ます。

2.  拡張機能が、指定された NIC 用に保存する実行時データを保持している場合は、そのデータを[**NDIS\_スイッチ\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)に保存します。これにより、構造体の先頭から*SaveDataOffset*バイトで始まる\_状態構造が保存されます。 次に、拡張機能は、NDIS\_STATUS\_SUCCESS の OID メソッド要求を完了します。

3.  [**Ndis\_スイッチ\_NIC\_SAVE\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体では、ランタイム状態を保持するのに十分なバッファーが提供されていない場合、拡張機能は、メソッド構造体の*Bytesneeded*フィールドを NDIS に設定し **\_SIZEOF\_NDIS\_スイッチ\_\_NIC を使用して\_状態\_リビジョン\_1 を保存**し、保存データを保持するために必要なバッファーの量を加算し、 **NDIS\_STATUS\_BUFFER で OID を完了します。\_\_短すぎ**ます。 OID は、必要なサイズで再発行されます。

4.  指定した NIC に対して保存する実行時データが拡張機能にない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す必要があります。 これにより、OID メソッド要求が拡張可能なスイッチドライバースタック内の基になるドライバーに転送されます。 この手順の詳細については、「 [NDIS フィルタードライバーでの OID 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。

拡張機能が実行時のポートデータを保存する場合は、次のガイドラインに従って、 [**NDIS\_スイッチ\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)内の実行時ポートデータを保存して\_状態構造を保存する必要があります。

1.  拡張機能は、ドライバーを一意に識別する GUID 値に**Extensionid**メンバーを設定します。
2.  拡張機能は、 **Extensionfriendlyname**メンバーをドライバーの名前に設定します。

    **  NDIS**\_スイッチ\_拡張機能\_FRIENDLYNAME データ型は\_文字列構造にカウントされ[**た場合**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)に、によって型が定義されます。 この構造体で定義された文字列は、null で終わる必要はありません。 ただし、文字列の長さは、この構造体の**length**メンバーで設定する必要があります。 文字列が NULL で終わる場合、**長さ**のメンバーに終端の null 文字を含めることはできません。     

3.  フィーチャークラスが保存されたランタイムデータに関連付けられている場合、拡張機能は、クラスを一意に識別する GUID を使用して**Featureclassid**を設定します。

    **注**  、保存されているランタイムデータにフィーチャークラスが関連付けられていない場合、拡張機能によって**featureclassid**が0に設定されます。     

4.  拡張機能は、ランタイムデータを**SaveData**メンバーにコピーし、実行時データのサイズ (バイト単位) に**savedatasize**メンバーを設定します。

**  拡張**機能では、NDIS\_スイッチの**ヘッダー**または**ポート id**メンバーを変更しないでください。 [ **\_NIC\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造を保存します。 

[Oid\_スイッチ\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)の oid メソッド要求は、最終的に、拡張可能スイッチの基になるミニポートエッジによって処理されます。 この OID メソッド要求が拡張可能なスイッチドライバースタックを介してミニポートドライバーに転送されると、ミニポートドライバーは、NDIS\_STATUS\_SUCCESS による OID 要求を完了します。 これにより、拡張可能スイッチのプロトコルエッジに、拡張可能なスイッチドライバースタックのすべての拡張機能が実行時ポートデータを照会したことが通知されます。 拡張可能なスイッチのプロトコルエッジは oid セットの要求を発行して、 [\_\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)を設定し、保存\_完了して保存操作を完了します。

### <a name="handling-the-oid_switch_nic_save_complete-request"></a>OID\_スイッチ\_NIC を処理する\_要求の完了\_保存

拡張可能なスイッチポートへのネットワークアダプター接続がある Hyper-v 子パーティションが一時停止されているか、その状態が保存されている場合、Hyper-v 拡張可能スイッチインターフェイスが通知されます。 これにより、拡張可能スイッチのプロトコルエッジで、Oid のオブジェクト識別子 (OID) メソッド要求が発行され、 [\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)が拡張可能なスイッチドライバースタック\_保存されます。 この手順の詳細については、「 [OID\_スイッチ\_NIC\_保存要求](handling-the-oid-switch-nic-save-request.md)」を参照してください。

すべての Hyper-v 拡張可能スイッチ拡張機能が実行時データを保存すると、拡張可能スイッチのプロトコルエッジは、保存操作が完了したことを基になる拡張機能に通知します。 プロトコルエッジは、Oid の OID セット要求を発行することによってこれを行います。 [\_スイッチ\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)し、拡張可能なスイッチドライバースタックを完了\_ます。

**注**  拡張可能なスイッチネットワークアダプター接続に対して実行時の保存操作を開始した場合、同じネットワークアダプター接続に対する別の保存操作は、 [OID が\_NIC\_切り替えるまで実行されません\_SAVE\_COMPLETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)要求が発行されました。 ただし、この間に他のネットワークアダプター接続の保存操作が発生する可能性があります。 

[**Ndis\_oid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)の**informationbuffer**メンバー\_oid\_スイッチに対する要求構造[\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)要求には、 [**ndis\_スイッチへのポインターが含まれて\_NIC\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造を保存します。 この構造体は、拡張可能スイッチのプロトコルエッジによって割り当てられます。

Oid の OID セット要求を受信すると[\_\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)すると、拡張機能は次のガイドラインに従う必要があります。

-   拡張機能では、OID 要求に関連付けられている\_状態の構造を[**保存\_\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)を変更することはできません。

-   拡張機能は、拡張可能なスイッチ拡張機能スタックを介してこの OID 要求を転送するために、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す必要があります。 拡張機能は OID 要求を失敗させることはできません。

    拡張機能では、この OID 要求の完了状態を監視する必要がある  に**注意**してください。 この拡張機能は、保存操作が正常に完了したかどうかを検出します。     

[Oid\_スイッチ\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)の oid メソッド要求は、保存\_完了\_、最終的には、拡張可能スイッチの基になるミニポートエッジによって処理されます。 この OID メソッド要求がミニポートエッジによって受信されると、NDIS\_STATUS\_SUCCESS による OID 要求が完了します。 これにより、拡張可能スイッチのプロトコルエッジに、拡張スイッチドライバースタックのすべての拡張機能が保存操作を完了したことが通知されます。

## <a name="restoring-hyper-v-extensible-switch-run-time-data"></a>Hyper-v 拡張可能スイッチ実行時データの復元

拡張可能なスイッチポートへのネットワークアダプター接続がある Hyper-v 子パーティションが一時停止から再開されると、Hyper-v 拡張可能スイッチインターフェイスが通知されます。 これにより、拡張可能スイッチのプロトコルエッジは、Oid のオブジェクト識別子 (OID) セット要求を発行し、 [\_NIC に\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)を設定し、拡張可能なスイッチドライバースタックを復元\_ます。 拡張機能は、この OID 要求を受信すると、子パーティションによって使用される拡張可能なスイッチポートの実行時データを復元できます。

[Oid\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)の[ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**INFORMATIONBUFFER**メンバーには、nic\_の\_\_スイッチへのポインターが含まれてい\_[ **\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造を保存します。 この構造体は、拡張可能スイッチのプロトコルエッジによって割り当てられます。

Oid の OID セット要求を受信すると[\_スイッチ\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)し、拡張可能なスイッチ拡張機能が実行時データを所有しているかどうかを最初に決定する必要があります。 この拡張機能では、NDIS\_スイッチの**Extensionid**メンバーの値を比較することによって、 [ **\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造を、拡張機能が自身を識別するために使用する GUID 値に比較します。

拡張可能なスイッチ NIC のランタイムデータが拡張機能によって所有されている場合は、次の方法でこのデータが復元されます。

1.  拡張機能は、 **SaveData**メンバーの実行時データをドライバーによって割り当てられたストレージにコピーします。

    **  ** NDIS\_スイッチの**ポート id**メンバーの値[ **\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造は、実行時データが保存された時点の**ポート id**値とは異なる場合があります。 これは、あるホストから別のホストへのライブマイグレーション中に実行時データが保存された場合に発生する可能性があります。 ただし、拡張可能スイッチ NIC の構成は、ライブマイグレーション中も保持されます。 これにより、拡張機能は、新しい**ポート id**値を使用して、実行時データを拡張可能スイッチ NIC に復元できます。     

2.  拡張機能は、NDIS\_STATUS\_SUCCESS の OID set 要求を完了します。

保存する指定されたランタイムデータが拡張機能によって所有されていない場合、拡張機能は[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出します。 これにより、OID セット要求が拡張可能なスイッチドライバースタック内の基になるドライバーに転送されます。 この場合、拡張機能では、OID 要求に関連付けられている\_状態の構造を[**保存\_\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)を変更することはできません。 OID 要求を転送する方法の詳細については、「 [NDIS フィルタードライバーでの Oid 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。

Oid の OID セット要求[\_スイッチ\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)が、NDIS\_STATUS\_SUCCESS によって完了すると、拡張可能スイッチのプロトコルエッジで別の OID セット要求が発行されます。 この新しい OID セット要求を受信すると、拡張機能は次のいずれかの操作を実行できます。

-   新しい OID 要求の実行時データを所有している場合は、拡張機能によって、 [**NDIS\_スイッチ\_NIC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)に追加の実行時データが復元され、\_状態構造が保存されます。 次に、拡張機能は、NDIS\_STATUS\_SUCCESS による OID 要求を完了します。

-   新しい OID 要求のランタイムデータを所有していない場合、拡張機能は[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、この oid セット要求を基になるドライバーに転送します。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_スイッチ\_NIC\_復元\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)  
拡張可能なスイッチインターフェイスは、拡張可能スイッチのプロトコルエッジに対して、拡張 switchnetwork アダプターの実行時データの復元操作の完了時にこの OID を発行するように通知します。

この OID 要求は、指定された拡張スイッチ NIC に対してのみ復元操作が完了したことを、拡張機能に通知します。

この OID 要求の詳細については、「 [oid\_SWITCH\_NIC\_復元\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)」を参照してください。

**注**  [oid\_SWITCH\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)セット要求が拡張スイッチのミニポートエッジによって受信された場合は、NDIS\_STATUS\_SUCCESS を使用して oid 要求を完了します。 これにより、拡張可能スイッチのプロトコルエッジに、ランタイムデータを所有している拡張機能がないことが通知されます。 このような場合は、拡張可能なスイッチインターフェイスによって、実行時ポートデータを最初に保存した拡張機能の**Extensionid**と**ポート id**メンバーの値を示すイベントがログに記録されます。