---
title: フィーダー スキャナーの子項目の要件
description: フィーダー スキャナーの子項目の要件
ms.assetid: 069ce228-ac73-42b5-9f1b-528ee6fe6a92
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b98c7cbb2af3bc7e08f5801bd48d6a7abb407725
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374261"
---
# <a name="requirements-for-feeder-scanners-child-items"></a>フィーダー スキャナーの子項目の要件


フィーダー スキャナー項目ツリー (つまり、フロント エンドとバックエンドの項目) の子項目は、ほとんどの項目のプロパティとフィーダー項目 (つまり、フロント エンドとバックエンドの項目の親項目) をサポートするフラグをサポートする必要があります。

### <a name="item-flags"></a>項目のフラグ

子項目をサポートする必要がありますすべてを除き、親項目でサポートされている必要な項目のフラグの**WiaItemTypeTransfer**します。 **WiaItemTypeTransfer**フラグは必要に応じてサポートされている可能性があります。 フィーダー項目と子項目ではなく外、ただし、自動ドキュメント フィーダーからのデータ転送を完了します。

### <a name="item-properties"></a>項目のプロパティ

フィーダー スキャナーの項目のツリー (またはフロント エンドとバックエンドの項目) の子項目が親フィーダー付きの項目をサポートする項目のプロパティのほとんどをサポートするために必要です。 子項目をサポートする必要があります[ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)とすべての WIA\_IP\_*Xxx*と WIA\_IPA\_*Xxx*フィーダー項目をサポートしています、現在のドキュメントの側の構成パラメーターのスキャンに関連するプロパティ。 これらのプロパティには、フィーダー項目で必須および省略可能なプロパティ両方にはが含まれます。 スキャナーでは、高度な双方向のスキャンを実行するときは、イメージ品質の設定 (またはスキャン構成パラメーター) 子項目で設定が使用され、フィーダー項目で設定したものは無視されます。

**注**  子項目のプロパティ項目の設定は親アイテムのプロパティの設定と一致する必要があります。 唯一の例外は、 [ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category) ; の子項目のプロパティ WIA をこのプロパティを設定する必要があります\_カテゴリ\_フィーダー\_前面または WIA\_カテゴリ\_フィーダー\_の代わりに WIA を\_カテゴリ\_送りします。

 

 

 




