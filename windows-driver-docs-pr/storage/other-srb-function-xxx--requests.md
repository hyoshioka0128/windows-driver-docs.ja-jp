---
title: その他の SRB_FUNCTION_XXX 要求
description: その他の SRB_FUNCTION_XXX 要求
ms.assetid: b0430d8e-e5cd-4f17-b77f-ec608b1469da
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_XXX 将来の使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e49772ea85345a30585d8d76f895d547cbd5d2d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384654"
---
# <a name="other-srbfunctionxxx-requests"></a>その他の SRB\_関数\_XXX 要求


## <span id="ddk_other_srb_function_xxx_requests_kg"></span><span id="DDK_OTHER_SRB_FUNCTION_XXX_REQUESTS_KG"></span>


次の SRB**関数**オペレーティング システムの将来のバージョンで使用するために値が定義されます。

-   SRB\_関数\_受信\_イベント

-   SRB\_関数\_リリース\_回復

-   SRB\_関数\_リセット\_デバイス

-   SRB\_関数\_TERMINATE\_IO

NT ベースのオペレーティング システムの SCSI ポート ドライバー次 SRB の要求を処理する**関数**SCSI ミニポート ドライバーを呼び出さずに値。

-   SRB\_関数\_要求\_デバイス

-   SRB\_関数\_リリース\_キュー

-   SRB\_関数\_フラッシュ\_キュー

-   SRB\_関数\_リリース\_デバイス

-   SRB\_関数\_ロック\_キュー

-   SRB\_関数\_UNLOCK\_キュー

詳細については、これらの関数は、次を参照してください。[ストレージ クラス ドライバー](storage-class-drivers.md)します。

ミニポート ドライバーのデザイナーは、ミニポート ドライバーが、想定できます*決して*、SRB、すぐに上記のいずれかで送信**関数**値。 NT ベースのオペレーティング システムのポート ドライバー HBA 固有 (またはミニポート ドライバー固有) にアクセスすることから高度なドライバーを保護する記憶域クラスおよびフィルター ドライバーからこれらの要求を処理する状態情報がデバイスを検索するかを取り消すキューに置かれた要求。 これにより、NT ベースのオペレーティング システムの記憶域クラスおよびフィルター ドライバーは、HBA の特殊なモデルでは依存関係がないこと。

参照してください[ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)詳細については、構造体。

 

 




