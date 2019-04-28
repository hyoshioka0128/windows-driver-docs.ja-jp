---
title: フィルム スキャナーの WIA 項目のフラグ
description: フィルム スキャナーの WIA 項目のフラグ
ms.assetid: 50aad730-6897-488d-a9de-58ce24738c17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a87701e76ad97c6d9ad81ae2f0f790ab110f2809
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363046"
---
# <a name="wia-item-flags-for-film-scanners"></a>フィルム スキャナーの WIA 項目のフラグ





このトピックでは、スキャナーのフィルム項目とスキャナー フィルムの子項目 (つまり、フレーム) に必要な WIA 項目フラグを使用します。 WIA 項目のフラグとその定義の完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)します。

### <a name="required-wia-item-flags-for-film-scanners"></a>WIA 項目フラグのフィルム スキャナーが必要

WIA フィルム スキャナーの項目が、次の WIA 項目フラグをサポートするために必要です。

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 項目は構成可能と一連の定義済み構成規則に基づく、 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)プロパティ。 フィルム スキャナーの一部のスキャンがプログラミング可能なために、このフラグが必要です。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 項目は、データ転送に使用できます。 データを転送するスキャナーのフィルムの項目を使用できるため、このフラグが必要です。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
項目は、ファイルです。 このフラグが必要ですが、 **WiaItemTypeImage**フラグ。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
項目は、イメージです。 このフラグは、フィルム スキャナーは、イメージ形式用を報告するために必要な[ **WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)プロパティの値。 (WIA が必要フィルム スキャナーのすべての項目が少なくとも 1 つのイメージ形式をサポートします。)WIA が現在必要ですが、WiaImgFmt\_BMP と WiaImgFmt\_MEMORYBMP イメージの形式がサポートされています。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
アイテムはフォルダーです。 このフラグは、個々 のフレームの列挙子項目を許可するルートのフィルムの項目に必要です。 (フレームは、画面をスキャンする 1 つのフィルムに選択した複数のリージョンを表します)。スキャナーのフィルム子項目 (フレーム)*できません*このフラグがあります。

 

 




