---
title: 既定のアロケーター
description: 既定のアロケーター
ms.assetid: ef61a33d-eabf-4449-8d11-cfd97aa2e403
keywords:
- 既定のアロケーター WDK カーネルストリーミング
- システムメモリアロケーター WDK カーネルストリーミング
- メモリアロケーター WDK のカーネルストリーミング
- 複数の送信先シンク WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 909caddd024b17301ff0da74ffcf1f75aad3cd9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837715"
---
# <a name="default-allocators"></a>既定のアロケーター





既定のアロケーターは、システムメモリからデータを転送し、特定のメモリ割り当てプロパティを必要とするデバイスドライバーのシステムメモリアロケーターを提供します。 既定のアロケーターを使用する場合、フィルターはアロケーター要件要求だけを処理する必要があります。

既定のアロケーターを使用する場合、ミニドライバーは、関連する[**ksallocator\_フレーミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)構造の**要件フラグ**メンバーで、KSALLOCATOR\_REQUIREMENTF\_SYSTEM\_MEMORY フラグを設定する必要があります。 IRP\_MJ\_CREATE が送信され、作成の種類が KSK CREATE\_要求\_アロケーターである場合、フィルターは[**KsCreateDefaultAllocator**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedefaultallocator)関数を呼び出すことによって、irp を既定のアロケーターハンドラーに転送します。 残りのすべての処理は、既定のアロケーターによって処理されます。

 

 




