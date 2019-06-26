---
title: Storport I/O モデルでのスキャッター/ギャザー リストへのアクセス
description: Storport I/O モデルでのスキャッター/ギャザー リストへのアクセス
ms.assetid: db05ac58-3317-44b2-9550-e4520537955f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cfcad79729c6b80383fd70c8983e496e3781c8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386299"
---
# <a name="access-to-scattergather-lists-in-the-storport-io-model"></a>Storport I/O モデルでのスキャッター/ギャザー リストへのアクセス


## <span id="ddk_access_to_scatter_gather_lists_in_the_storport_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI ポート ドライバーが、メモリ範囲を定義するスキャッター/ギャザー リスト構造体のセットと、SRB の物理アドレスに完全にアクセスします。 ただし、SCSI ポート ドライバーと連動するミニポート ドライバーは必要ありません。 SCSI ポート I/O モデルで、強制的に、ミニポート ドライバーを手動で検出し、繰り返しの呼び出しを通じて、独自のスキャッター/ギャザー リストを構築、 [ **ScsiPortGetPhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetphysicaladdress)ルーチン。

Storport の I/O モデルでは、ミニポート ドライバーがドライバー サポート ルーチンのポートをそのプライベート スキャッター/ギャザーの一覧を作成するが呼び出しの数を減らすと、システムのスキャッター/ギャザー リスト構造に直接アクセスできる、ミニポート ドライバーを提供します。

スキャッター/ギャザーを一覧表示する[ **StorPortGetScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetscattergatherlist) SRB が完了するまでのみが有効な値を取得します。

ミニポート ドライバーがスキャッター/ギャザーを一覧表示するには、メモリを解放する必要はありません**StorPortGetScatterGatherList**を返します。

ミニポート ドライバーが Storport ミニポート ドライバーのミニポート ドライバー固有の書式をからに提供スキャッター/ギャザー リストの必要な変換を実行する必要があります[ **HwStorBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)ルーチン。

 

 




