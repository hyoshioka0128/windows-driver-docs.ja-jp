---
title: Hyper-V 拡張可能スイッチの復元操作
description: Hyper-V 拡張可能スイッチの復元操作
ms.assetid: 283D9E43-79F2-47B1-8D29-39A8E7CBE2C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f62b393d709e525d3a653dbcb46b0c9a11751b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349516"
---
# <a name="hyper-v-extensible-switch-restore-operations"></a>Hyper-V 拡張可能スイッチの復元操作


停止しているか、ライブ移行した後、HYPER-V 子パーティションが再起動されると、パーティションの実行時の状態が復元されます。 HYPER-V 拡張可能スイッチの拡張機能ドライバーは、復元操作中に、拡張可能スイッチのネットワーク アダプター (NIC) の実行時のデータを復元できます。

要求を設定するときに、復元操作が実行される HYPER-V 子パーティションでは、拡張可能スイッチのインターフェイスは拡張可能スイッチのプロトコルの端を通知 OID を発行する[OID\_切り替える\_NIC\_復元](https://msdn.microsoft.com/library/windows/hardware/hh598268)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710) OID の構造体\_スイッチ\_NIC\_復元要求にはへのポインターが含まれています、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体。

この OID 要求を処理する場合、拡張機能は、ネットワーク アダプターの実行時のデータを復元します。 OID 要求の実行時データが以前に保存した[OID\_スイッチ\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)と OID\_スイッチ\_NIC\_保存\_完了します。

受信した場合、 [OID\_切り替える\_NIC\_復元](https://msdn.microsoft.com/library/windows/hardware/hh598267)、拡張可能スイッチ拡張機能が、実行時のデータが所有しているかどうかを判断する必要があります最初の要求。 ドライバーの値と比較することによって、 **ExtensionId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)ドライバーを使用して自身を識別する GUID 値構造体。

拡張機能が実行時のデータを所有している場合は、次のようにこのデータが復元されます。

1.  拡張機能の実行時データのコピー、 **SaveData**ドライバーに割り当てられたストレージへのメンバー。

    **注**  の値、 **PortId**のメンバー、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体が異なる可能性があります、 **PortId**実行時データの保存時の値。 これは、実行時のデータが別のホストへのライブ マイグレーションを実行中に保存された場合に発生することができます。 ただし、ライブ マイグレーション中に、拡張可能スイッチの NIC の構成が保持されます。 これにより、拡張可能スイッチの NIC を新しいを使用して、実行時データを復元する拡張機能**PortId**値。

     

2.  拡張機能は、NDIS を使用して、OID のセット要求を完了\_状態\_成功します。

呼び出す必要がありますが、拡張機能が実行時のデータを所有していない場合[ **NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)します。 これは、基になる拡張機能は拡張可能スイッチ ドライバー スタックの OID メソッド要求を転送します。 この手順の詳細については、次を参照してください。 [NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)します。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_スイッチ\_NIC\_復元\_完了](https://msdn.microsoft.com/library/windows/hardware/hh846215)  
拡張可能スイッチのインターフェイスの拡張可能スイッチの NIC の実行時のデータの復元操作の完了時に、この OID を発行する拡張可能スイッチ プロトコルのエッジを通知します。

この OID 要求は、拡張機能の拡張可能スイッチを指定した NIC に対してのみ復元操作が完了したことを通知します

この OID 要求の詳細については、次を参照してください。 [OID\_スイッチ\_NIC\_復元\_完了](https://msdn.microsoft.com/library/windows/hardware/hh846215)します。

実行時のデータの復元操作中に拡張可能スイッチのプロトコルのエッジの問題の OID 要求[OID\_切り替える\_NIC\_復元](https://msdn.microsoft.com/library/windows/hardware/hh598267)と[OID\_スイッチ\_NIC\_復元\_完了](https://msdn.microsoft.com/library/windows/hardware/hh846215)HYPER-V 子のネットワーク インターフェイスのパーティションが接続されています。 複数の HYPER-V 子パーティションが復元される場合、プロトコルの edge 問題個別の OID\_スイッチ\_NIC\_復元と OID\_スイッチ\_NIC\_復元\_各ネットワーク インターフェイスの接続要求を完了します。

**注**  拡張可能スイッチのプロトコルのエッジは復元操作を実行時のデータを同じ nic をインターリーブ プロトコルのエッジは、前回の復元操作が同じ NIC で完了した後にのみ、NIC の実行時のデータの復元操作は開始します。 ただし、プロトコル edge 可能性があります、復元操作を開始 NIC の別の復元操作の進行中はもう 1 つの nic このため、強くお勧めの拡張機能が非インターリーブ方式で復元操作を実行します。 たとえば、拡張機能を想定しないでください別の NIC の継続的な復元操作が完了する前に別の NIC では、復元処理を開始できません。

 

この OID 要求の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ実行時データを復元](restoring-hyper-v-extensible-switch-run-time-data.md)します。

 

 





