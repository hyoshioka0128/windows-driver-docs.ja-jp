---
title: Storport の SRB と記憶域クラス ドライバーとのインターフェイス
description: Storport の SRB と記憶域クラス ドライバーとのインターフェイス
ms.assetid: c7e55516-0ba9-48bc-9b68-e6344552f070
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3884a56c03c423cd0da91762ffeb4021f37b9181
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842832"
---
# <a name="storports-srb-interface-with-the-storage-class-driver"></a>Storport の SRB と記憶域クラス ドライバーとのインターフェイス


記憶域クラスドライバーおよびその他の上位レベルのコンポーネントは、SCSI 要求ブロック (SRBs) を構築することによって、Storport ドライバーと通信します。 SRB には、SCSI コマンド記述子ブロック (CDB) と、デバイスとの間でデータを転送するために使用されるデータバッファーへのポインター (存在する場合) が含まれています。 SCSI の sense データを保持するために使用される sense バッファーへのポインターが含まれている場合があります。 SRBs の詳細については、「 [**SCSI\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)」を参照してください。 ストレージクラスドライバーは、 **MajorFunction**メンバーが IRP\_MJ\_SCSI に設定されている irp で、作成した SRBs を Storport に渡します。 ストレージクラスドライバーがポートドライバーに渡す前に SRB を構築するために必要な手順の説明については、「[ストレージクラスドライバーの BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)」を参照してください。

SRB をスタックに転送する前に、Storport は、パス、ターゲット番号、ターゲットデバイスの論理ユニット番号など、SRB 内の特定の値を設定します。

IDE/ATAPI および IEEE 1394 バス用のシステム指定のポートドライバーなどの他のポートドライバーとは異なり、Storport では、SRBs でコマンド記述子ブロック (CDB) を変換してから、それを別の形式に転送してから、基になるアダプター。 Storport は、ターゲット固有のいくつかの情報を SRB に追加し、CDB を変更せずにミニポートドライバーに渡します。 そのため、Storport は、CDBs を含む SRBs をスタックに渡すだけです。

このため、ストレージクラスドライバーと Storport 間の SRB インターフェイスのほとんどの側面については、ストレージクラスと記憶域ミニポートドライバーに関する一般的なドキュメントと、それらに付随する参考資料を参照してください。 ストレージクラスドライバーと Storport ミニポートドライバーのペア間の SRB インターフェイスに関連するセクションの一覧については、「storport[のインターフェイスと Storport ミニポートドライバー](storport-s-interface-with-storport-miniport-drivers.md)」を参照してください。

 

 




