---
title: SCSI ポートの SRB と記憶域クラス ドライバーとのインターフェイス
description: SCSI ポートの SRB と記憶域クラス ドライバーとのインターフェイス
ms.assetid: ca30bf9b-6d76-4160-8a4e-54c681dfc843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a46fb4501c966f6cc00ae1e0c68c2b669019fda9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363366"
---
# <a name="scsi-ports-srb-interface-with-the-storage-class-driver"></a>SCSI ポートの SRB と記憶域クラス ドライバーとのインターフェイス


## <span id="ddk_scsi_ports_srb_interface_with_the_storage_class_driver_kg"></span><span id="DDK_SCSI_PORTS_SRB_INTERFACE_WITH_THE_STORAGE_CLASS_DRIVER_KG"></span>


ストレージ クラス ドライバーおよびその他の上位レベルのコンポーネントは、SCSI 要求のブロック (される Srb) を構築することにより、SCSI ポート ドライバーと通信します。 される Srb の詳細については、次を参照してください。 [ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)します。 ストレージ クラスのドライバーでは、自分で作成される Srb を渡すと IRP の SCSI ポートに、 **MajorFunction**メンバー IRP に設定\_MJ\_SCSI です。 ストレージ クラス ドライバーが行う必要のある手順の説明についてはポート ドライバーに渡す前に、SRB をビルドする参照[記憶域クラス ドライバー BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)します。

下位のスタック、SRB を転送する前に、SCSI ポートは、ポート番号、パス、目標の数、および対象デバイスの論理ユニット番号など、SRB の特定の値を設定します。

IDE/ATAPI、IEEE 1394 のバスのシステムが指定したポート ドライバーなどの他のポート ドライバーとは異なり SCSI ポートにしていないコマンド記述子ブロック (CDB) を変換するに転送する前に別の形式に受信したされる Srb、基になるアダプター。 SCSI ポートは、SRB にいくつかのターゲット固有の情報を追加し、ミニポート ドライバーに cdb をそのまま渡しますだけです。 したがって、SCSI ポートは、下位のスタック Cdb が含まれているされる Srb を通過する messenger だけです。

このため、記憶域クラス ドライバーと SCSI ポート間の SRB インターフェイスのほとんどの側面はストレージ クラスとストレージ ミニポート ドライバーとその付属の参考資料の全般的なドキュメントについて説明します。 記憶域クラス ドライバーおよび SCSI ポート ミニポート ドライバーのペア間 SRB インターフェイスに関連するセクションの一覧は、次を参照してください。 [SCSI ポート ミニポート ドライバーと SCSI ポートのインターフェイス](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)します。

 

 




