---
title: フィルム スキャナーの WIA 項目のフラグ
description: フィルム スキャナーの WIA 項目のフラグ
ms.assetid: 50aad730-6897-488d-a9de-58ce24738c17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f963b16c2d98554fd5304408fc1de2ac93f73252
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383071"
---
# <a name="wia-item-flags-for-film-scanners"></a>フィルム スキャナーの WIA 項目のフラグ





このトピックでは、スキャナーのフィルム項目とスキャナー フィルムの子項目 (つまり、フレーム) に必要な WIA 項目フラグを使用します。 WIA 項目のフラグとその定義の完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)します。

### <a name="required-wia-item-flags-for-film-scanners"></a>WIA 項目フラグのフィルム スキャナーが必要

WIA フィルム スキャナーの項目が、次の WIA 項目フラグをサポートするために必要です。

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 項目は構成可能と一連の定義済み構成規則に基づく、 [ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)プロパティ。 フィルム スキャナーの一部のスキャンがプログラミング可能なために、このフラグが必要です。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 項目は、データ転送に使用できます。 データを転送するスキャナーのフィルムの項目を使用できるため、このフラグが必要です。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
項目は、ファイルです。 このフラグが必要ですが、 **WiaItemTypeImage**フラグ。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
項目は、イメージです。 このフラグは、フィルム スキャナーは、イメージ形式用を報告するために必要な[ **WIA\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)プロパティの値。 (WIA が必要フィルム スキャナーのすべての項目が少なくとも 1 つのイメージ形式をサポートします。)WIA が現在必要ですが、WiaImgFmt\_BMP と WiaImgFmt\_MEMORYBMP イメージの形式がサポートされています。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
アイテムはフォルダーです。 このフラグは、個々 のフレームの列挙子項目を許可するルートのフィルムの項目に必要です。 (フレームは、画面をスキャンする 1 つのフィルムに選択した複数のリージョンを表します)。スキャナーのフィルム子項目 (フレーム)*できません*このフラグがあります。

 

 




