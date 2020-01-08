---
title: その他の SRB_FUNCTION_XXX 要求
description: その他の SRB_FUNCTION_XXX 要求
ms.assetid: b0430d8e-e5cd-4f17-b77f-ec608b1469da
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- 将来の使用 SRB_FUNCTION_XXX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 246d8673ab9942c67a38233f4ce01d13ef36c1af
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606508"
---
# <a name="other-srb_function_xxx-requests"></a>その他の SRB_FUNCTION_XXX 要求

次の SRB**関数**の値は、将来のバージョンのオペレーティングシステムで使用するために定義されています。

- SRB_FUNCTION_RECEIVE_EVENT

- SRB_FUNCTION_RELEASE_RECOVERY

- SRB_FUNCTION_RESET_DEVICE

- SRB_FUNCTION_TERMINATE_IO

NT ベースのオペレーティングシステムの SCSI ポートドライバーは、SCSI ミニポートドライバーを呼び出さずに、次の SRB**関数**の値を持つ要求を処理します。

- SRB_FUNCTION_CLAIM_DEVICE

- SRB_FUNCTION_RELEASE_QUEUE

- SRB_FUNCTION_FLUSH_QUEUE

- SRB_FUNCTION_RELEASE_DEVICE

- SRB_FUNCTION_LOCK_QUEUE

- SRB_FUNCTION_UNLOCK_QUEUE

これらの関数の詳細については、「[ストレージクラスドライバー](introduction-to-storage-class-drivers.md)」を参照してください。

ミニポートドライバーの設計者は、そのミニポートドライバーが、直前の**関数**の値のいずれかと共に SRB に送信されることを想定でき*ませ*ん。 NT ベースのオペレーティングシステムポートドライバーは、これらの要求をストレージクラスおよびフィルタードライバーから処理して、上位レベルのドライバーが、HBA 固有 (またはミニポートドライバー固有) の状態情報にアクセスしてデバイスを検索したり、キャンセルしたりすることを防止します。キューに置かれた要求。 これにより、NT ベースのオペレーティングシステムの記憶域クラスとフィルタードライバーは、特定のモデルの HBA に依存しなくなります。

詳細については[**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)構造を参照してください。
