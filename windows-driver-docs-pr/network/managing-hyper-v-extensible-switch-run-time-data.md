---
title: Hyper-V 拡張可能スイッチ実行時データの管理
description: Hyper-V 拡張可能スイッチ実行時データの管理
ms.assetid: 08A353F5-D8CB-4645-9337-8169D302F6F2
ms.date: 12/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: c65fbe0d02f6da64d5dcb70913f1b44c90783e2c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356161"
---
# <a name="managing-hyper-v-extensible-switch-run-time-data"></a>Hyper-V 拡張可能スイッチ実行時データの管理

このトピックでは、保存について説明し、復元操作の HYPER-V 拡張可能スイッチの拡張機能。 これらの操作では、保存し、個々 の拡張可能スイッチのネットワーク adapters(NICs) の実行時データの復元の拡張機能を許可します。 拡張可能スイッチ ポートにネットワーク アダプターの接続を持つ HYPER-V 子パーティションがされているときに、これらの操作は実行が停止または開始します。

## <a name="saving-hyper-v-extensible-switch-run-time-data"></a>HYPER-V 拡張可能スイッチの実行時データの保存

このセクションでは、HYPER-V 拡張可能スイッチの拡張機能が個々 のネットワーク アダプター (Nic) の実行時データを保存する操作について説明します。 この操作は、拡張可能スイッチ ポートにネットワーク アダプターの接続を備えた HYPER-V 子パーティションを停止していますか、その状態は保存されているときに実行されます。

### <a name="handling-the-oidswitchnicsave-request"></a>OID の処理\_スイッチ\_NIC\_保存要求

拡張可能スイッチ ポートにネットワーク アダプターの接続を備えた HYPER-V 子パーティションが停止しているか、その状態を保存、HYPER-V 拡張可能スイッチのインターフェイスが通知されます。 これにより、拡張可能スイッチのオブジェクト識別子 (OID) メソッド要求を発行するためのプロトコルのエッジ[OID\_スイッチ\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)拡張可能スイッチのドライバー スタックのダウンします。 拡張可能スイッチの拡張機能は、この OID 要求を受信したときに、子パーティションに関連付けられている指定されたネットワーク アダプターの接続の場合は、その実行時データを節約できます。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)用の構造、 [OID\_スイッチ\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)要求にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。 この構造体では、拡張可能スイッチのプロトコルの端で割り当てられ、次のように初期化することが。

-   **ヘッダー** revisionof、現在の型を格納するメンバーが初期化されて、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。 サイズは、完全なバッファーのサイズに設定されます。

-   **PortId**メンバーでは、拡張可能スイッチ ポートの一意の識別子を格納する、保存操作が実行されます。

受信した場合、 [OID\_スイッチ\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)メソッドの要求、拡張機能は次の処理します。

1.  拡張機能の読み取り、 **PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。

2.  内でそのデータを保存、拡張機能に指定した NIC について保存する実行時データがある場合、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)以降では構造体*SaveDataOffset*構造体の先頭からのバイト数。 拡張機能は、NDIS に OID メソッド要求を完了\_状態\_成功します。

3.  場合、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体は、拡張機能のランタイム状態を保持するための十分なバッファーを提供していない、拡張機能設定メソッドの構造体の*BytesNeeded*フィールドを**NDIS\_SIZEOF\_NDIS\_スイッチ\_NIC\_保存\_状態\_リビジョン\_1**さらに、保存を保持するために必要なバッファーの量、データの OID が完了して**NDIS\_状態\_バッファー\_すぎる\_短い**します。 OID が必要なサイズで再発行されます。

4.  呼び出す必要がありますが、拡張子が指定した NIC について保存する実行時データを持たない場合[ **NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)します。 これは、拡張可能スイッチ ドライバー スタック内の基になるドライバーに OID メソッド要求を転送します。 この手順の詳細については、次を参照してください。 [NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)します。

内のポートの実行時データを保存するときにガイドラインに従ってする必要がありますが、拡張機能に保存する実行時にポート データがある場合、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。

1.  拡張機能セット、 **ExtensionId**メンバー、ドライバーを一意に識別する GUID 値にします。
2.  拡張機能セット、 **ExtensionFriendlyName**メンバー、ドライバーの名前にします。

    **注**  、NDIS\_スイッチ\_拡張子\_FRIENDLYNAME データ型は、型定義、 [**場合\_カウント済\_文字列**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)構造体。 この構造体で定義されている文字列が null で終了する必要はありません。 ただし、文字列の長さ設定する必要があります、**長さ**この構造体のメンバー。 文字列が NULL で終わる場合、**長さ**メンバーは、終端の NULL 文字を含めることはできません。     

3.  機能クラスを保存済みの実行時データに関連付けられた場合、拡張機能の設定、 **FeatureClassId**クラスを一意に識別する GUID を持つ。

    **注**  機能クラスで保存済みの実行時データに関連付けられてない場合、拡張機能の設定、 **FeatureClassId**をゼロにします。     

4.  拡張機能を実行時データのコピー、 **SaveData**メンバー、セット、 **SaveDataSize**サイズ、実行時データのバイト単位のメンバー。

**注**  、拡張機能の変更はできません、**ヘッダー**または**PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。 

OID メソッド要求[OID\_切り替える\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)拡張可能スイッチの基になるミニポート edge によって最終的に処理されます。 ミニポート ドライバーで NDIS OID 要求が完了するとこの OID メソッド要求は、拡張可能スイッチ ドライバー スタックを通じたミニポート ドライバーに転送されていますと\_状態\_成功します。 ポートの実行時データの拡張可能スイッチ ドライバー スタック内のすべての拡張機能をクエリが実行されている拡張可能スイッチのプロトコルの端に通知します。 拡張可能スイッチのプロトコルのエッジの OID セットの要求を発行し、 [OID\_切り替える\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)保存を完了する操作。

### <a name="handling-the-oidswitchnicsavecomplete-request"></a>OID の処理\_スイッチ\_NIC\_保存\_完全な要求

拡張可能スイッチ ポートにネットワーク アダプターの接続を持つ HYPER-V 子パーティションが一時停止したり、その状態は保存されている、HYPER-V 拡張可能スイッチのインターフェイスが通知されます。 これにより、拡張可能スイッチのオブジェクト識別子 (OID) メソッド要求を発行するためのプロトコルのエッジ[OID\_スイッチ\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)拡張可能スイッチのドライバー スタックのダウンします。 この手順の詳細については、次を参照してください。 [OID を処理\_スイッチ\_NIC\_保存要求](handling-the-oid-switch-nic-save-request.md)します。

すべての HYPER-V 拡張可能スイッチの拡張機能では、その実行時データを保存した、拡張可能スイッチのプロトコルの端に通知基になる拡張機能を保存操作が完了しました。 プロトコルのエッジの OID セット要求を発行することによって[OID\_切り替える\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)拡張可能スイッチのドライバー スタックの下します。

**注**  まで同じネットワーク アダプターの接続は実行されませんの操作を保存別、拡張可能スイッチのネットワーク アダプター接続の開始されると、保存操作の実行時、 [OID\_スイッチ\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)要求を発行します。 ただし、接続がこの期間中に発生する可能性があります、その他のネットワーク アダプターの操作を保存します。 

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)用の構造、 [OID\_スイッチ\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)要求にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。 この構造体は、拡張可能スイッチのプロトコル edge によって割り当てられます。

OID のセット要求を受け取ったとき[OID\_スイッチ\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)、拡張機能が次のガイドラインに従う必要があります。

-   拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) OID 要求に関連付けられている構造体。

-   拡張機能を呼び出す必要があります[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)拡張可能スイッチ拡張機能のスタックを通じてこの OID 要求を転送します。 拡張機能では、OID 要求が失敗しない必要があります。

    **注**  拡張機能は、この OID 要求の完了ステータスを監視する必要があります。 拡張機能はこれを検出するかどうか、保存操作が正常に完了します。     

OID メソッド要求[OID\_切り替える\_NIC\_保存\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)拡張可能スイッチの基になるミニポート edge によって最終的に処理されます。 NDIS に OID 要求が完了するミニポート edge によってこの OID メソッド要求を受信すると、\_状態\_成功します。 拡張可能スイッチのプロトコルの端に通知、拡張可能スイッチ ドライバー スタック内のすべての拡張機能が、保存を完了している操作。

## <a name="restoring-hyper-v-extensible-switch-run-time-data"></a>HYPER-V 拡張可能スイッチの実行時データを復元します。

拡張可能スイッチ ポートにネットワーク アダプターの接続を持つ HYPER-V 子パーティションが停止状態から再開され、HYPER-V 拡張可能スイッチのインターフェイスが通知されます。 これにより、拡張可能スイッチのオブジェクト識別子 (OID) セット要求を発行するためのプロトコルのエッジ[OID\_スイッチ\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)拡張可能スイッチのドライバー スタックのダウンします。 拡張機能は、この OID 要求を受信したときに、子パーティションによって使用される拡張可能スイッチ ポートの場合は、その実行時データを復元できます。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)用の構造、 [OID\_スイッチ\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)要求にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。 この構造体は、拡張可能スイッチのプロトコル edge によって割り当てられます。

OID のセット要求を受け取ったとき[OID\_切り替える\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)、拡張可能スイッチ拡張機能が実行時のデータが所有しているかどうかを判断する必要がありますまずします。 値を比較することでこの拡張機能の実行、 **ExtensionId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体を拡張機能を使用して自身を識別する GUID 値。

拡張機能が拡張可能スイッチ NIC の実行時データを所有している場合は、次のようにこのデータが復元されます。

1.  拡張機能の実行時データのコピー、 **SaveData**ドライバーに割り当てられたストレージへのメンバー。

    **注**  の値、 **PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体が異なる可能性があります、 **PortId**実行時データの保存時の値。 これは、実行時のデータが別のホストへのライブ マイグレーションを実行中に保存された場合に発生することができます。 ただし、ライブ マイグレーション中に、拡張可能スイッチの NIC の構成が保持されます。 これにより、拡張可能スイッチの NIC を新しいを使用して、実行時データを復元する拡張機能**PortId**値。     

2.  拡張機能は、NDIS を使用して、OID のセット要求を完了\_状態\_成功します。

拡張機能が保存する指定された実行時データを所有していない場合、拡張機能を呼び出す[ **NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)します。 これは、拡張可能スイッチ ドライバー スタック内の基になるドライバーに OID のセット要求を転送します。 この場合、拡張機能は変更しないで、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) OID 要求に関連付けられている構造体。 OID 要求を転送する方法の詳細については、次を参照してください。 [NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)します。

OID の要求を設定する場合は[OID\_切り替える\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)NDIS が完了しました\_状態\_成功すると、拡張可能スイッチのプロトコル edge 問題別。OID は、要求を設定します。 この新しい OID セット要求を受信した場合、拡張機能は、次のいずれかを実行できます。

-   拡張機能が内で追加の実行時データを復元する新しい OID 要求の実行時データを所有しているが場合、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造体。 拡張機能は、NDIS に OID 要求を完了\_状態\_成功します。

-   拡張機能を呼び出す場合は、新しい OID 要求の実行時のデータを所有していない、 [ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)この OID を転送するには、基になるドライバーに要求を設定します。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_スイッチ\_NIC\_復元\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)  
拡張可能スイッチのインターフェイスは、拡張可能な switchnetwork アダプターの実行時のデータの復元操作の完了時に、この OID を発行する拡張可能スイッチのプロトコルの端を通知します。

この OID 要求は、拡張機能の拡張可能スイッチを指定した NIC に対してのみ復元操作が完了したことを通知します

この OID 要求の詳細については、次を参照してください。 [OID\_スイッチ\_NIC\_復元\_完了](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)します。

**注**  場合、 [OID\_切り替える\_NIC\_復元](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)セット要求を受信した拡張可能スイッチのミニポート エッジ、NDIS に OID 要求が完了します。\_状態\_成功します。 これによって、拡張機能に、実行時データが所有していないことに拡張可能スイッチのプロトコルの端に通知します。 拡張可能スイッチのインターフェイスを記載したイベントをログにこのような場合、 **ExtensionId**と**PortId**ポート データの最初の実行時に保存された拡張機能のメンバーの値。