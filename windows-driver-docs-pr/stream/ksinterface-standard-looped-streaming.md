---
title: KSK インターフェイス\_STANDARD\_ループ\_ストリーミング
description: KSK インターフェイス\_STANDARD\_ループ\_ストリーミング
ms.assetid: c12e7085-fa13-48d3-b4ed-ea0a708f026b
keywords:
- KSINTERFACE_STANDARD_LOOPED_STREAMING ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSINTERFACE_STANDARD_LOOPED_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925deb2d8f0ca73d6389e3bf051517eeefa8f846
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838867"
---
# <a name="ksinterface_standard_looped_streaming"></a>KSK インターフェイス\_STANDARD\_ループ\_ストリーミング


## <span id="ddk_ksinterface_standard_looped_streaming_ks"></span><span id="DDK_KSINTERFACE_STANDARD_LOOPED_STREAMING_KS"></span>


DSound のクライアントでは、KSK インターフェイス\_標準\_ループ\_STREAMING インターフェイスが使用されます。 Windows XP のリリース時に、Kmixer と Portcls は、このインターフェイスをサポートする唯一の KS オーディオフィルターです。

Pin が KSK インターフェイス\_標準\_ループ\_ストリーミングをサポートしている場合、関連するフィルターは、pin が*停止*状態になるまでバッファーを完了しません。 フィルターは、フィルターに送信された1つのバッファー内のデータを連続してループすることで、データを処理します。

### <a name="see-also"></a>参照

[Ksinterfacesetid\_Standard](ksinterfacesetid-standard.md)、 [**KSPIN\_INTERFACE**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))、 [**kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)

 

 





