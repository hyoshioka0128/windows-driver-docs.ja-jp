---
title: Storport I/O モデルでのスキャッター/ギャザー リストへのアクセス
description: Storport I/O モデルでのスキャッター/ギャザー リストへのアクセス
ms.assetid: db05ac58-3317-44b2-9550-e4520537955f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb2869588ac800e24bf7262c194d6169dc6f2e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845539"
---
# <a name="access-to-scattergather-lists-in-the-storport-io-model"></a>Storport I/O モデルでのスキャッター/ギャザー リストへのアクセス


## <span id="ddk_access_to_scatter_gather_lists_in_the_storport_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI ポートドライバーは、SRB のメモリ範囲と物理アドレスを定義する一連のスキャッター/ギャザーリスト構造に完全にアクセスできます。 ただし、SCSI ポートドライバーで動作するミニポートドライバーは使用できません。 SCSI ポート i/o モデルでは、 [**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)ルーチンを繰り返し呼び出すことによって、ミニポートドライバーが手動で検出し、独自のスキャッター/ギャザーリストを構築するように強制します。

Storport i/o モデルは、システムのスキャッター/ギャザーリスト構造に直接アクセスできるようにミニポートドライバーを提供します。これにより、ミニポートドライバーは、プライベートなスキャッター/ギャザーリストを構築するために、ポートドライバーサポートルーチンに対して必要な呼び出しの回数を減らすことができます。

[**StorPortGetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetscattergatherlist)が返すスキャッター/ギャザーリストは、SRB が完了するまで有効です。

ミニポートドライバーは、 **StorPortGetScatterGatherList**から返されるスキャッター/ギャザーリストのメモリを解放する必要はありません。

ミニポートドライバーは、Storport によって提供されるスキャッター/ギャザーリストをミニポートドライバーの[**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)ルーチンでミニポートドライバー固有の形式に変換する必要があります。

 

 




