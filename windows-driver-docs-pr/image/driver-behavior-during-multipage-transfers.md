---
title: 複数ページ転送中のドライバーの動作
description: 複数ページ転送中のドライバーの動作
ms.assetid: ecf0428b-c11c-49ff-9aa3-322e55dbca07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed082e893d753e1b11a8b16b8b5be0d4fc3c5af9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385037"
---
# <a name="driver-behavior-during-multipage-transfers"></a>複数ページ転送中のドライバーの動作


ドライバーは、フォルダーの取得を直接サポートする必要はありません。 項目のツリーと呼び出しを説明しますドライバーが、これもサポートしていない場合、WIA サービスは再帰的に[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)を持つすべてのアイテムで、 **WiaItemTypeTransfer**ビットが設定、 [ **WIA\_IPA\_項目\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)プロパティ。

フォルダーの取得を直接サポートするドライバーが公開する必要があります、 [ **WIA\_IP\_転送\_機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-transfer-capabilities)フォルダー項目のプロパティ。 このプロパティは、WIA をする必要がありますが、フラグ プロパティ\_転送\_ACQUIRE\_子\_対応ビットがフォルダーの取得機能を直接サポートしているかを示す設定。 このサポートにより、WIA サービスを呼び出すだけですが、ドライバー自体に関連するアイテムを転送するツリーはについて説明します**IWiaMiniDrv::drvAcquireItemData**フォルダー。 ドライバーと区別できます通常転送要求フォルダーの取得要求をテストして、 *lFlags*パラメーター、WIA を\_転送\_ACQUIRE\_子ビット。

ドライバーがフォルダーの取得を直接サポートは、主な理由の 1 つは、効率性です。 ドライバーは、複数の項目の各アイテムの転送を呼び出す、WIA サービスよりもはるかに効率化を転送場合があります。

このような状況の良い例は、マルチリー ジョンのスキャン中には。 スキャナーのフラット ベッドで (個別の写真) などの複数のリージョンが検出されると、「フラット ベッド」項目に子として表すことができます。 このような状況の例は、次の図で表現されます。

![マルチリー ジョンをスキャンするため、項目のツリーを示す図](images/itemtree-multiregionscan.png)

「フラット ベッド」の子項目ごとに個別の転送が呼び出された場合、ドライバーは時間のかかる 3 つの個別のスキャンを実行します。 ただし、フォルダーの取得が「フラット ベッド」で要求された場合、ドライバーは 1 つのスキャンを実行、分解、して返す (これは、多くの場合、高速) 3 つの異なるリージョン。

**注**  をお勧めより高度なドライバーは、フォルダーの取得を直接サポート、ドライバーが項目のツリーをウォークし、適切な操作を行うためです。

 

 

 




