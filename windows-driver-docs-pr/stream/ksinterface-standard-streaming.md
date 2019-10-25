---
title: KSK インターフェイス\_STANDARD\_STREAMING
description: KSK インターフェイス\_STANDARD\_STREAMING
ms.assetid: 04ba6879-1699-4d12-b81e-a90878014325
keywords:
- KSINTERFACE_STANDARD_STREAMING ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSINTERFACE_STANDARD_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e29062db17a3675cbf5bd03b4adc073136b7f73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838865"
---
# <a name="ksinterface_standard_streaming"></a>KSK インターフェイス\_STANDARD\_STREAMING


## <span id="ddk_ksinterface_standard_streaming_ks"></span><span id="DDK_KSINTERFACE_STANDARD_STREAMING_KS"></span>


KSK インターフェイス\_STANDARD\_STREAMING インターフェイスは、ほとんどののオーディオフィルター間で使用され、すべてのオーディオミニポートでサポートされています。 Pin でこのインターフェイスがサポートされている場合、関連するフィルターは、各 Ksk ストリームに埋め込まれているデータを[ **\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体に1回処理します。

### <a name="see-also"></a>参照

[Ksinterfacesetid\_Standard](ksinterfacesetid-standard.md)、 [**KSPIN\_INTERFACE**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))、 [**kspin\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)、 [**ksstream\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)

 

 





