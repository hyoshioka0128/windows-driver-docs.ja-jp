---
title: Storport でのハードウェアの初期化
description: Storport でのハードウェアの初期化
ms.assetid: 98930338-d192-4b25-a558-01614ef9662b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97dfe054da0a59d71589effdb39fd323027bc681
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838001"
---
# <a name="hardware-initialization-with-storport"></a>Storport でのハードウェアの初期化


## <span id="ddk_hardware_initialization_with_storport_kg"></span><span id="DDK_HARDWARE_INITIALIZATION_WITH_STORPORT_KG"></span>


Storport ドライバーは、SCSI ポートドライバーのプラグアンドプレイ (PnP) 初期化モデルに従います。 ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンでは、ミニポートドライバーは、サポートしているハードウェアを説明する[**HW\_初期化\_データ (STORPORT)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data)構造を使用して[**storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)ルーチンを呼び出します。 その後、PnP マネージャーがポートドライバーの[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンを呼び出すと、ポートドライバーは[**ポート\_CONFIGURATION\_INFORMATION (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))構造を使用してミニポートドライバーの[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)ルーチンを呼び出します。ミニポートドライバーの[**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)ルーチンを呼び出して、アダプターを初期化します。

ほとんどの場合、Storport バージョンの HW\_初期化\_データ構造は、SCSI ポートで使用されるのと同じ名前の構造と同じです。

「 [Storport I/o モデルでのマッピングバッファーの使用](use-of-mapping-buffers-in-the-storport-i-o-model.md)」セクションで示されているように、HW\_の初期化とポート\_構成\_情報の両方の**mapbuffers**メンバーは、storport の場合とは異なる意味を持ちます。SCSI ポートの場合は、

 

 




