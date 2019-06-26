---
title: Storport でのハードウェアの初期化
description: Storport でのハードウェアの初期化
ms.assetid: 98930338-d192-4b25-a558-01614ef9662b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d9257ed8560924a9d9148975bae17b20177d7a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371154"
---
# <a name="hardware-initialization-with-storport"></a>Storport でのハードウェアの初期化


## <span id="ddk_hardware_initialization_with_storport_kg"></span><span id="DDK_HARDWARE_INITIALIZATION_WITH_STORPORT_KG"></span>


Storport ドライバーでは、SCSI ポート ドライバーのプラグ アンド プレイ (PnP) の初期化のモデルに従います。 ドライバーの中に[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ミニポート ドライバーのルーチンを呼び出し、 [ **StorPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize) ルーチン[ **HW\_初期化\_データ (STORPORT)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_hw_initialization_data)をサポートするハードウェアを記述する構造体。 以降、PnP マネージャーが、ポート ドライバーを呼び出すときに[ **StartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ポート ドライバー呼び出し、ミニポート ドライバーの日常的な[ **HwStorFindAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)ルーチンを[**ポート\_構成\_情報 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))ミニポート ドライバーへの呼び出しに続く構造[ **HwStorInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)ルーチン アダプターを初期化します。

Storport バージョン、ハードウェアのほとんどの場合、\_初期化\_SCSI ポートで使用される同じ名前で構造体の場合と同じデータ構造です。

セクションに記載されている[使用のマッピング内のバッファー、Storport の I/O モデル](use-of-mapping-buffers-in-the-storport-i-o-model.md)、 **MapBuffers** HW 両方のメンバー\_初期化とポート\_構成\_情報は、SCSI ポートの場合から Storport の場合も異なる意味を持ちます。

 

 




