---
title: Storport でのハードウェアの初期化
description: Storport でのハードウェアの初期化
ms.assetid: 98930338-d192-4b25-a558-01614ef9662b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ddc1f047cb2a079d3943c88dae361c72608735
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383109"
---
# <a name="hardware-initialization-with-storport"></a>Storport でのハードウェアの初期化


## <span id="ddk_hardware_initialization_with_storport_kg"></span><span id="DDK_HARDWARE_INITIALIZATION_WITH_STORPORT_KG"></span>


Storport ドライバーでは、SCSI ポート ドライバーのプラグ アンド プレイ (PnP) の初期化のモデルに従います。 ドライバーの中に[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ミニポート ドライバーのルーチンを呼び出し、 [ **StorPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff567108) ルーチン[ **HW\_初期化\_データ (STORPORT)** ](https://msdn.microsoft.com/library/windows/hardware/ff557459)をサポートするハードウェアを記述する構造体。 以降、PnP マネージャーが、ポート ドライバーを呼び出すときに[ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ポート ドライバー呼び出し、ミニポート ドライバーの日常的な[ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)ルーチンを[**ポート\_構成\_情報 (STORPORT)** ](https://msdn.microsoft.com/library/windows/hardware/ff563901)ミニポート ドライバーへの呼び出しに続く構造[ **HwStorInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff557396)ルーチン アダプターを初期化します。

Storport バージョン、ハードウェアのほとんどの場合、\_初期化\_SCSI ポートで使用される同じ名前で構造体の場合と同じデータ構造です。

セクションに記載されている[使用のマッピング内のバッファー、Storport の I/O モデル](use-of-mapping-buffers-in-the-storport-i-o-model.md)、 **MapBuffers** HW 両方のメンバー\_初期化とポート\_構成\_情報は、SCSI ポートの場合から Storport の場合も異なる意味を持ちます。

 

 




