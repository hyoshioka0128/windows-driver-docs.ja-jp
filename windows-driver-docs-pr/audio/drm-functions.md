---
title: DRM の関数
description: DRM の関数
ms.assetid: 7be96ab4-3c27-4e63-b0dd-71d814d804d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23df55369de4062f0d62bb58e2473524555dc512
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833437"
---
# <a name="drm-functions"></a>DRM の関数


## <span id="ddk_drm_functions_ks"></span><span id="DDK_DRM_FUNCTIONS_KS"></span>


このセクションでは、Windows でカーネルストリーミングオーディオコンテンツのデジタル著作権を管理するために使用される DRM 機能について説明します。 システムドライバーコンポーネント Drmk. sys には、これらの関数のエントリポイントが含まれています。 これらの関数の定義は、ヘッダーファイル drmk. h に表示されます。 詳細については、「 [Digital Rights Management](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)」を参照してください。

このセクションでは、次の DRM 機能について説明します。

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmaddcontenthandlers)

[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmcreatecontentmixed)

[**DrmDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmdestroycontent)

[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttofileobject)

[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmgetcontentrights)

さらに、このセクションでは、次のマクロについて説明します。

[**既定\_\_DRMRIGHTS を定義する**](https://docs.microsoft.com/previous-versions/ff536254(v=vs.85))

 

 





