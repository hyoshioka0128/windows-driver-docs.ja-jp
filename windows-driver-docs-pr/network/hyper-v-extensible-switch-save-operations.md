---
title: Hyper-V 拡張可能スイッチの保存操作
description: Hyper-V 拡張可能スイッチの保存操作
ms.assetid: 7148B094-2551-4035-A6BE-141DD01BEA14
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 576c4caef1b964d7695d5c69a6a88cde4a16f6d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349494"
---
# <a name="hyper-v-extensible-switch-save-operations"></a>Hyper-V 拡張可能スイッチの保存操作


HYPER-V 子パーティションは、停止、保存されている、またはライブ移行、パーティションの実行時の状態が保存されます。 保存中に操作を HYPER-V 拡張可能スイッチの拡張機能は、拡張可能スイッチのネットワーク アダプター (NIC) の実行時のデータを保存できます。

保存時に操作が実行される HYPER-V 子パーティションでは、拡張可能スイッチのインターフェイスは、操作に関する拡張機能を通知します。 拡張機能は、次のオブジェクト識別子 (OID) 要求で通知されます。

<a href="" id="oid-switch-nic-save"></a>[OID\_スイッチ\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)  
保存中にこの OID を発行する拡張可能スイッチのプロトコルの端を通知する拡張可能スイッチのインターフェイスの拡張可能スイッチの NIC の操作 この OID 要求を処理する場合、拡張機能が NIC の実行時のデータを返します 実行時のデータを保存すると後の OID のセット要求を通じた復元[OID\_スイッチ\_NIC\_復元](https://msdn.microsoft.com/library/windows/hardware/hh598267)します。

受信した場合、 [OID\_スイッチ\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)メソッド要求を拡張機能は、次のいずれかを行うことができます。

-   拡張機能に保存する実行時データがある場合は、初期化、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造体であり、さまざまな設定メンバーなど、 **ExtensionId**自体とそれを保存するデータを識別するために、メンバー。 拡張機能内のデータを保存します、 **NDIS\_スイッチ\_NIC\_保存\_状態**、構造体の先頭から開始 SaveDataOffset バイト構造体と完了。NDIS に OID メソッド要求\_状態\_成功します。

-   場合、 [ **NDIS\_スイッチ\_NIC\_保存\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598216)構造が NDISで列挙、十分なバッファーサイズを提供していない\_オブジェクト\_ヘッダー**サイズ**、拡張機能の実行時状態を保持するためにメンバー セットのメソッドの構造体の*BytesNeeded*フィールド NDIS を\_SIZEOF\_NDIS\_スイッチ\_NIC\_保存\_状態\_リビジョン\_1 および保存を保持するために必要なバッファーのデータ、NDIS に OID が完了して\_ステータス\_バッファー\_すぎます\_短い。 必要なサイズの OID を再発行します。
-   呼び出す必要がありますが、拡張機能では、実行時のデータを保存することはない場合、 [ **NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)します。 これは、基になる拡張機能は拡張可能スイッチ ドライバー スタックの OID メソッド要求を転送します。 この手順の詳細については、次を参照してください。 [NDIS フィルター ドライバーでの OID 要求のフィルタ リング](filtering-oid-requests-in-an-ndis-filter-driver.md)します。

この OID 要求の詳細については、次を参照してください。[処理 OID\_スイッチ\_NIC\_保存要求](handling-the-oid-switch-nic-save-request.md)します。

<a href="" id="oid-switch-nic-save-complete"></a>[OID\_スイッチ\_NIC\_保存\_完了](https://msdn.microsoft.com/library/windows/hardware/hh598268)  
拡張可能スイッチのインターフェイス、保存の完了時に、この OID を発行する拡張可能スイッチのプロトコルの端を通知する拡張可能スイッチの NIC の実行時のデータの操作

この OID 要求が、拡張機能を通知するファイルの指定した拡張可能スイッチの NIC に対してのみ操作が完了しました。

この OID 要求の詳細については、次を参照してください。[処理 OID\_スイッチ\_NIC\_保存\_要求を完了](handling-the-oid-switch-nic-save-complete-request.md)します。

保存中に実行時のデータの操作は、拡張可能スイッチのプロトコルのエッジがの OID 要求を発行する[OID\_切り替える\_NIC\_保存](https://msdn.microsoft.com/library/windows/hardware/hh598268)と OID\_切り替える\_NIC\_保存\_HYPER-V 子パーティションのネットワーク インターフェイスが接続されているを完了します。 プロトコルのエッジの問題が OID のセットを分離する場合は、複数の HYPER-V 子パーティションが停止している、またはライブ移行、\_スイッチ\_NIC\_の保存および OID\_スイッチ\_NIC\_保存\_完全な要求の各ネットワーク インターフェイスの接続。

**注**  拡張可能スイッチのプロトコルの端をインターリーブ保存実行時のデータの操作を同一の NIC には プロトコルのエッジは、同じ NIC で以前保存操作が完了した後にのみ、保存、NIC の操作の実行時のデータは開始します。 プロトコルのエッジが、保存を開始するただし、別の保存操作中に、NIC の操作がもう 1 つの NIC の進行状況 このため、強くお勧め保存操作が非インターリーブ方式で拡張機能を実行することです。 たとえば、拡張機能を想定しないでください、新しい保存操作を開始できませんもう 1 つの NIC で別の NIC の中で保存操作が完了する前に、

 

 

 





