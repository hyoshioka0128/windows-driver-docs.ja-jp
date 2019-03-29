---
title: DRM の関数
description: DRM の関数
ms.assetid: 7be96ab4-3c27-4e63-b0dd-71d814d804d7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 619ae36d96ca1f7e7ba16255731a754aaa72b6f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573130"
---
# <a name="drm-functions"></a>DRM の関数


## <span id="ddk_drm_functions_ks"></span><span id="DDK_DRM_FUNCTIONS_KS"></span>


このセクションでは、ドライバーが Windows でのカーネル ストリーミングのオーディオ コンテンツのデジタル著作権管理を使用して、DRM 関数について説明します。 システム ドライバー コンポーネント Drmk.sys には、これらの関数のエントリ ポイントが含まれています。 ヘッダー ファイル drmk.h でこれらの関数の定義が表示されます。 詳細については、次を参照してください。[デジタル著作権管理](https://msdn.microsoft.com/library/windows/hardware/ff536260)します。

このセクションでは、次の DRM 関数について説明します。

[**DrmAddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff536347)

[**DrmCreateContentMixed**](https://msdn.microsoft.com/library/windows/hardware/ff536348)

[**DrmDestroyContent**](https://msdn.microsoft.com/library/windows/hardware/ff536349)

[**DrmForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff536351)

[**DrmForwardContentToFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff536352)

[**DrmForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff536353)

[**DrmGetContentRights**](https://msdn.microsoft.com/library/windows/hardware/ff536354)

さらに、このセクションでは、次のマクロについて説明します。

[**DEFINE\_DRMRIGHTS\_DEFAULT**](https://msdn.microsoft.com/library/windows/hardware/ff536254)

 

 





