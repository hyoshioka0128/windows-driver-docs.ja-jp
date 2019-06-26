---
title: WIA 項目のフラグ
description: WIA 項目のフラグ
ms.assetid: 2b96bc23-705b-47f0-811c-1cb4a8be8b34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1cd223387112c94ef6e661e640969fce2cb0499
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383067"
---
# <a name="wia-item-flags"></a>WIA 項目のフラグ





このトピックには、Windows Vista 以降が適用されます。

WIA 項目のフラグは、コンテンツを分類するために使用されますか、WIA の特定のアイテムの動作がサポートされています。 WIA 項目のフラグは、2 つの基本的なグループに分類されます。

<a href="" id="item-status-flags"></a>項目の状態フラグ  
WIA 項目の現在の状態を報告するフラグ。

次に、例を示します。**WiaItemTypeDisconnected**、 **WiaItemTypeDeleted**など。

<a href="" id="item-data-representation-usage-flags"></a>項目のデータ表現/使用状況のフラグ  
データを表しますまたは転送される場合に生成できる項目の WIA を報告するフラグ。

次に、例を示します。**WiaItemTypeImage** WIA の現在の項目に関連付けられているデータをアプリケーションに通知するデータ表現フラグはイメージ データであり、イメージ データ プロパティがあります。 **WiaItemTypeProgrammableDataSource** WIA 項目が構成可能な一連の定義済みの構成ルールに基づいてアプリケーションに示す項目使用法フラグには、 [ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)、および構成の各データ転送結果を変更できる可能性があります。 参照してください[WIA 項目カテゴリ](wia-item-categories.md)カテゴリ定義の詳細についてはします。

WIA 項目のフラグとその定義の完全な一覧については、次を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)します。

 

 




