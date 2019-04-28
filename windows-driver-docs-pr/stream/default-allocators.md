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
ms.openlocfilehash: 05aa025a46e2fa3f00e6b777bfdc846cfa244e75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374099"
---
# <a name="default-allocators"></a>既定のアロケーター





既定のアロケーターは、システム メモリからデータを転送するデバイス ドライバーのシステムのメモリ アロケーターを提供し、特定のメモリ割り当てのプロパティを必要とします。 既定のアロケーターを使用する場合、フィルター必要がありますのみ要求を処理、アロケーター要件。

既定のアロケーターを使用して、ミニドライバーは、KSALLOCATOR を設定する必要があります\_REQUIREMENTF\_システム\_メモリ フラグ、 **RequirementsFlags**の関連メンバー [ **KSALLOCATOR\_フレーム**](https://msdn.microsoft.com/library/windows/hardware/ff560979)構造体。 ときに IRP\_MJ\_作成が送信され、作成の種類が KSCREATE\_要求\_呼び出してアロケーター、フィルターの転送 IRP が既定のアロケーター ハンドラーに、 [ **KsCreateDefaultAllocator** ](https://msdn.microsoft.com/library/windows/hardware/ff561641)関数。 残りのすべての処理は、既定のアロケーターによって処理されます。

 

 




