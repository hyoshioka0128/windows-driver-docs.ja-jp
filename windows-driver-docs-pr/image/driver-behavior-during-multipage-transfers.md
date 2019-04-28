---
title: 複数ページ転送中のドライバーの動作
description: 複数ページ転送中のドライバーの動作
ms.assetid: ecf0428b-c11c-49ff-9aa3-322e55dbca07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c5d0fd08773bbf980c24bbc4469fc622cf746ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364513"
---
# <a name="driver-behavior-during-multipage-transfers"></a>複数ページ転送中のドライバーの動作


ドライバーは、フォルダーの取得を直接サポートする必要はありません。 項目のツリーと呼び出しを説明しますドライバーが、これもサポートしていない場合、WIA サービスは再帰的に[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)を持つすべてのアイテムで、 **WiaItemTypeTransfer**ビットが設定、 [ **WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)プロパティ。

フォルダーの取得を直接サポートするドライバーが公開する必要があります、 [ **WIA\_IP\_転送\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff552657)フォルダー項目のプロパティ。 このプロパティは、WIA をする必要がありますが、フラグ プロパティ\_転送\_ACQUIRE\_子\_対応ビットがフォルダーの取得機能を直接サポートしているかを示す設定。 このサポートにより、WIA サービスを呼び出すだけですが、ドライバー自体に関連するアイテムを転送するツリーはについて説明します**IWiaMiniDrv::drvAcquireItemData**フォルダー。 ドライバーと区別できます通常転送要求フォルダーの取得要求をテストして、 *lFlags*パラメーター、WIA を\_転送\_ACQUIRE\_子ビット。

ドライバーがフォルダーの取得を直接サポートは、主な理由の 1 つは、効率性です。 ドライバーは、複数の項目の各アイテムの転送を呼び出す、WIA サービスよりもはるかに効率化を転送場合があります。

このような状況の良い例は、マルチリー ジョンのスキャン中には。 スキャナーのフラット ベッドで (個別の写真) などの複数のリージョンが検出されると、「フラット ベッド」項目に子として表すことができます。 このような状況の例は、次の図で表現されます。

![マルチリー ジョンをスキャンするため、項目のツリーを示す図](images/itemtree-multiregionscan.png)

「フラット ベッド」の子項目ごとに個別の転送が呼び出された場合、ドライバーは時間のかかる 3 つの個別のスキャンを実行します。 ただし、フォルダーの取得が「フラット ベッド」で要求された場合、ドライバーは 1 つのスキャンを実行、分解、して返す (これは、多くの場合、高速) 3 つの異なるリージョン。

**注**  をお勧めより高度なドライバーは、フォルダーの取得を直接サポート、ドライバーが項目のツリーをウォークし、適切な操作を行うためです。

 

 

 




