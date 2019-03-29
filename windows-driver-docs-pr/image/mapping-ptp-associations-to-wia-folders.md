---
title: WIA フォルダーへの PTP 関連付けのマッピング
description: WIA フォルダーへの PTP 関連付けのマッピング
ms.assetid: 81de26fd-1f93-4018-a628-ad0b0d7468ba
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6a5f9d49f3f00532de84626825da128ff4033a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574097"
---
# <a name="mapping-ptp-associations-to-wia-folders"></a>WIA フォルダーへの PTP 関連付けのマッピング





ほとんどのオブジェクトの関連付けには、PTP ドライバーは、WIA フォルダーの項目を作成します。 WIA\_IPA\_項目\_この表に示すように、フラグのプロパティがアソシエーションの種類に応じてさまざまなフラグを設定します。

PTP 関連付けコード アソシエーション型 WIA 項目型フラグ (Windows SDK のドキュメントで説明) 0x0000

未定義

WiaItemTypeFolder

0x0001

GenericFolder

WiaItemTypeFolder

0x0002

アルバム

WiaItemTypeFolder

0x0003

TimeSequence

WiaItemTypeFolder |WiaItemTypeBurst

0x0004

HorizontalPanoramic

WiaItemTypeFolder |WiaItemTypeHPanorama

0x0005

VerticalPanoramic

WiaItemTypeFolder | WiaItemTypeVPanorama

0x0006

2DPanoramic

WiaItemTypeFolder

0x0007

AncillaryData

テキストに付属するを参照してください。

 

**SequenceNumber** ObjectInfo データセットのフィールドは、WIA 入れる\_IPC\_シーケンス プロパティ。 PTP ドライバーが、WIA を現在使用していない\_IPC\_XCOORDINATE と WIA\_IPC\_YCOORDINATE プロパティ。 **AssociationDesc** ObjectInfo データセットのメンバーが使用されません。

次の図は、カメラに格納されている AncillaryData アソシエーション例を示します。 この関連付けは、関連付けられているオーディオ、テキストとイメージで構成されます。

![補助的なデータを使用したイメージの ptp ツリー](images/ptp.png)

AncillaryData アソシエーションが WIA フォルダーにマッピングされると、次の図に示すように非イメージ オブジェクト、イメージ オブジェクトの子になります。 イメージ オブジェクトが WIA で設定 WiaItemTypeHasAttachments フラグ\_IPA\_項目\_フラグ。

![wia 項目の添付ファイル](images/wiaattch.png)

 

 




