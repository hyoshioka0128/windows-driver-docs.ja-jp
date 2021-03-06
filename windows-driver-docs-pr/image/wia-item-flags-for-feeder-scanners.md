---
title: フィーダー スキャナーの WIA 項目のフラグ
description: フィーダー スキャナーの WIA 項目のフラグ
ms.assetid: b1256646-be6c-436c-86da-9dff43ef9867
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67f74710bae83513aabfda7ccc0a74d82307cc0c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383073"
---
# <a name="wia-item-flags-for-feeder-scanners"></a>フィーダー スキャナーの WIA 項目のフラグ





このトピックでは、スキャナーのフィーダー項目とスキャナー フィーダー子項目 (フロントとバック ページ項目) の必須および省略可能な WIA 項目フラグを使用します。 WIA 項目のフラグとその定義の完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)します。

### <a name="required-wia-item-flags-for-feeder-scanners"></a>WIA 項目がフィーダー スキャナーのフラグが必要

次の WIA 項目のフラグをサポートするために、WIA フィーダー スキャナーの項目が必要です。

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 項目は構成可能と一連の定義済み構成規則に基づく、 [ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)プロパティ。 スキャナーのドキュメント フィーダーがプログラミング可能なために、このフラグが必要です。

<a href="" id="wiaitemtypetransfer-"></a>**WiaItemTypeTransfer**   
WIA 項目は、データ転送に使用できます。 データを転送する項目のツリーで、スキャナーのフィーダー項目を使用できるため、このフラグが必要です。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
項目は、ファイルです。 このフラグが必要ですが、 **WiaItemTypeImage**フラグ。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
項目は、イメージです。 このフラグは設定されている項目でのみ有効です、 **WiaItemTypeFile**フラグを設定します。 スキャナーのドキュメント フィーダー付きのイメージ形式のレポート、 [ **WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)プロパティの値。 (WIA である必要があります*すべて*フィーダー スキャナーの項目が少なくとも 1 つのイメージ形式をサポートします)。WIA が WiaImgFmt 現在必要があります\_BMP と WiaImgFmt\_MEMORYBMP としてサポートされているイメージ形式。

### <a name="optional-wia-item-flags-for-feeder-scanners"></a>WIA の省略可能なアイテムがフィーダー スキャナーをフラグします。

WIA フィーダー スキャナーの項目は、次 WIA 項目フラグを必要に応じてサポートできます。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
アイテムはフォルダーです。 このフラグは、自動ドキュメント フィーダーがフロント エンドとバックエンドの項目をサポートしている場合、ルート項目必要があります。 このフラグは、子項目として列挙の前面とページの背面を使用します。 子項目*できません*このフラグがあります。

 

 




