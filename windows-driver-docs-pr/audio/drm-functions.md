---
title: DRM の関数
description: DRM の関数
ms.assetid: 7be96ab4-3c27-4e63-b0dd-71d814d804d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a521d86630171325d3e2fa2cbc4719c563a592a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360097"
---
# <a name="drm-functions"></a>DRM の関数


## <span id="ddk_drm_functions_ks"></span><span id="DDK_DRM_FUNCTIONS_KS"></span>


このセクションでは、ドライバーが Windows でのカーネル ストリーミングのオーディオ コンテンツのデジタル著作権管理を使用して、DRM 関数について説明します。 システム ドライバー コンポーネント Drmk.sys には、これらの関数のエントリ ポイントが含まれています。 ヘッダー ファイル drmk.h でこれらの関数の定義が表示されます。 詳細については、次を参照してください。[デジタル著作権管理](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)します。

このセクションでは、次の DRM 関数について説明します。

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmaddcontenthandlers)

[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmcreatecontentmixed)

[**DrmDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmdestroycontent)

[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttofileobject)

[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmgetcontentrights)

さらに、このセクションでは、次のマクロについて説明します。

[**DEFINE\_DRMRIGHTS\_DEFAULT**](https://docs.microsoft.com/previous-versions/ff536254(v=vs.85))

 

 





