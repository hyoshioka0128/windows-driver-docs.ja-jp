---
title: その他の SRB_FUNCTION_XXX 要求
description: その他の SRB_FUNCTION_XXX 要求
ms.assetid: b0430d8e-e5cd-4f17-b77f-ec608b1469da
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- 将来使用する SRB_FUNCTION_XXX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b41f49529b06ff831fce2f6fe0d9da4af8bc542e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842734"
---
# <a name="other-srb_function_xxx-requests"></a>その他の SRB\_関数\_XXX 要求


## <span id="ddk_other_srb_function_xxx_requests_kg"></span><span id="DDK_OTHER_SRB_FUNCTION_XXX_REQUESTS_KG"></span>


次の SRB**関数**の値は、将来のバージョンのオペレーティングシステムで使用するために定義されています。

-   SRB\_関数\_受信\_イベント

-   SRB\_関数\_リリース\_回復

-   SRB\_関数\_リセット\_デバイス

-   SRB\_関数\_終了\_IO

NT ベースのオペレーティングシステムの SCSI ポートドライバーは、SCSI ミニポートドライバーを呼び出さずに、次の SRB**関数**の値を持つ要求を処理します。

-   SRB\_関数\_要求\_デバイス

-   SRB\_関数\_リリース\_キュー

-   SRB\_関数\_フラッシュ\_キュー

-   SRB\_関数\_リリース\_デバイス

-   SRB\_関数\_ロック\_キュー

-   SRB\_関数\_\_キューのロック解除

これらの関数の詳細については、「[ストレージクラスドライバー](storage-class-drivers.md)」を参照してください。

ミニポートドライバーの設計者は、そのミニポートドライバーが、直前の**関数**の値のいずれかと共に SRB に送信されることを想定でき*ませ*ん。 NT ベースのオペレーティングシステムポートドライバーは、これらの要求をストレージクラスおよびフィルタードライバーから処理して、上位レベルのドライバーが、HBA 固有 (またはミニポートドライバー固有) の状態情報にアクセスしてデバイスを検索したり、キャンセルしたりすることを防止します。キューに置かれた要求。 これにより、NT ベースのオペレーティングシステムの記憶域クラスとフィルタードライバーは、特定のモデルの HBA に依存しなくなります。

詳細については、「 [**SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)の構造」を参照してください。

 

 




