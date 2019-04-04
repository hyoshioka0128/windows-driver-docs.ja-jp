---
title: 記憶域クラス ドライバーを使用した、Storport の SRB インターフェイス
description: 記憶域クラス ドライバーを使用した、Storport の SRB インターフェイス
ms.assetid: c7e55516-0ba9-48bc-9b68-e6344552f070
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4020cba407f002f60b92aa2b62b0757ffd3dff78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537529"
---
# <a name="storports-srb-interface-with-the-storage-class-driver"></a>記憶域クラス ドライバーを使用した、Storport の SRB インターフェイス


ストレージ クラス ドライバーおよびその他の上位レベルのコンポーネントは、SCSI 要求のブロック (される Srb) を構築することにより、Storport ドライバーと通信します。 SRB には、SCSI コマンド記述子ブロック (CDB) および (存在する場合)、デバイス間でデータの転送に使用するデータ バッファーへのポインターが含まれています。 条件の確認の状態で SCSI コマンドが失敗したイベントには、SCSI センス データを保持するために使用される意味バッファーへのポインターに含めることができます。 される Srb の詳細については、[ **SCSI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565393)を参照してください。 記憶域クラス ドライバーが Storport の IRP でに自分で作成される Srb を渡す、 **MajorFunction**メンバー IRP に設定\_MJ\_SCSI です。 ストレージ クラス ドライバーが行う必要のある手順の説明についてはポート ドライバーに渡す前に、SRB をビルドする参照[記憶域クラス ドライバー BuildRequest ルーチン](storage-class-driver-s-buildrequest-routine.md)します。

下位のスタック、SRB を転送する前に、Storport は、パス、目標の数、ターゲット デバイスの論理ユニット番号など、SRB の特定の値を設定します。

IDE/ATAPI、IEEE 1394 のバスのシステムが指定したポート ドライバーなどの他のポート ドライバーとは異なり Storport にしていないコマンド記述子ブロック (CDB) を変換する別の形式にして、転送する前に受信したされる Srb、基になるアダプター。 Storport は単に、SRB にいくつかのターゲット固有の情報を追加し、cdb をそのままミニポート ドライバーに渡します。 そのため、Storport は下位のスタック Cdb が含まれているされる Srb を渡すだけです。

このため、記憶域クラス ドライバー、Storport と SRB インターフェイスのほとんどの側面はストレージ クラスとストレージ ミニポート ドライバーとその付属の参考資料の全般的なドキュメントについて説明します。 記憶域クラス ドライバーおよび Storport ミニポート ドライバーのペア間 SRB インターフェイスに関連するセクションの一覧は、[Storport ミニポート ドライバー、Storport のインターフェイス](storport-s-interface-with-storport-miniport-drivers.md)を参照してください。

 

 




