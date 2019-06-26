---
title: 既定のアロケーター
description: 既定のアロケーター
ms.assetid: ef61a33d-eabf-4449-8d11-cfd97aa2e403
keywords:
- 既定のアロケーターの WDK カーネルがストリーミング
- システム メモリ アロケーター WDK カーネル ストリーミング
- ストリーミング メモリ アロケーター WDK カーネル
- 複数の変換先は、WDK カーネルのストリーミングをシンクします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 006d4d6a5cf7224dd0be5796f080259a562d2458
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376391"
---
# <a name="default-allocators"></a>既定のアロケーター





既定のアロケーターは、システム メモリからデータを転送するデバイス ドライバーのシステムのメモリ アロケーターを提供し、特定のメモリ割り当てのプロパティを必要とします。 既定のアロケーターを使用する場合、フィルター必要がありますのみ要求を処理、アロケーター要件。

既定のアロケーターを使用して、ミニドライバーは、KSALLOCATOR を設定する必要があります\_REQUIREMENTF\_システム\_メモリ フラグ、 **RequirementsFlags**の関連メンバー [ **KSALLOCATOR\_フレーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksallocator_framing)構造体。 ときに IRP\_MJ\_作成が送信され、作成の種類が KSCREATE\_要求\_呼び出してアロケーター、フィルターの転送 IRP が既定のアロケーター ハンドラーに、 [ **KsCreateDefaultAllocator** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatedefaultallocator)関数。 残りのすべての処理は、既定のアロケーターによって処理されます。

 

 




