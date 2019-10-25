---
title: SCSI ポートの SRB と記憶域クラス ドライバーとのインターフェイス
description: SCSI ポートの SRB と記憶域クラス ドライバーとのインターフェイス
ms.assetid: ca30bf9b-6d76-4160-8a4e-54c681dfc843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10fc2d1bbe9fca50459c7aa8e38b849b5de66817
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842652"
---
# <a name="scsi-ports-srb-interface-with-the-storage-class-driver"></a>SCSI ポートの SRB と記憶域クラス ドライバーとのインターフェイス


## <span id="ddk_scsi_ports_srb_interface_with_the_storage_class_driver_kg"></span><span id="DDK_SCSI_PORTS_SRB_INTERFACE_WITH_THE_STORAGE_CLASS_DRIVER_KG"></span>


記憶域クラスドライバーおよびその他の上位レベルのコンポーネントは、SCSI 要求ブロック (SRBs) を構築することによって、SCSI ポートドライバーと通信します。 SRBs の詳細については、「 [**SCSI\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)」を参照してください。 ストレージクラスドライバーは、作成した SRBs を IRP の SCSI ポートに渡します。この場合、 **MajorFunction**メンバーが IRP\_MJ\_scsi に設定されます。 ストレージクラスドライバーがポートドライバーに渡す前に SRB を構築するために必要な手順の説明については、「[ストレージクラスドライバーの BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)」を参照してください。

SCSI ポートは、SRB をスタックに転送する前に、ポート番号、パス、ターゲット番号、ターゲットデバイスの論理ユニット番号など、SRB 内の特定の値を設定します。

IDE/ATAPI および IEEE 1394 バス用のシステム指定のポートドライバーなどの他のポートドライバーとは異なり、SCSI ポートでは、SRBs でコマンド記述子ブロック (CDB) を変換してから、そのファイルを別の形式に転送してから、基になるアダプター。 SCSI ポートは、ターゲット固有のいくつかの情報を SRB に追加し、CDB を変更せずにミニポートドライバーに渡します。 したがって、SCSI ポートは、CDBs を含む SRBs をスタックに渡すだけの messenger です。

このため、ストレージクラスドライバーと SCSI ポート間の SRB インターフェイスのほとんどの側面については、ストレージクラスと記憶域ミニポートドライバーに関する一般的なドキュメントと、それらに付随する参考資料を参照してください。 ストレージクラスドライバーと SCSI ポート-ミニポートドライバーのペアの間の SRB インターフェイスに関連するセクションの一覧については、scsi ポート[のポートミニポートドライバーを使用した Scsi ポートのインターフェイス](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)に関するセクションを参照してください。

 

 




