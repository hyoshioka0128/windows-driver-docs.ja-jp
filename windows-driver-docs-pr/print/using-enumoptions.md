---
title: EnumOptions の使用
description: EnumOptions の使用
ms.assetid: 6ce16d28-eff7-4701-a592-046f364cda44
keywords:
- EnumOptions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ce4ebc7f2eb92905d5577525c3baf4a19654bf1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330290"
---
# <a name="using-enumoptions"></a>EnumOptions の使用





呼び出し元が使用できます**EnumOptions**サポートされているドライバーの機能、およびその PPD 機能するためのオプションのキーワードの一覧を取得します。 PPD 機能、 **EnumOptions**は常にサポートし、PPD. によって定義されているオプションを返します

ドライバーの機能の**EnumOptions**機能は現在サポートされていて、オプションの固定セットに対してのみサポートされます。 例: %addeuro が 2 つのオプション。"True"と"False"、および %pageorder は"FrontToBack"と"BackToFront"の 2 つのオプションがあります。 **EnumOptions**以上サポートされていて %addeuro (言語レベルが 2 の場合)、PageOrder % は、(スプーラー EMF スプールが有効になっている) 場合。 %Custompagesize、%psmemory、およびその他のユーザーなどの機能が無制限に使用可能なオプションは、つまり**EnumOptions**はそれらのサポートされていません。

現在サポートされていないドライバーの機能やサポートされているドライバー機能経由で列挙可能なない**EnumOptions**、 **EnumOptions**返します E\_NOTIMPL します。

また、ドライバーの機能のいくつかのオプションの条件下では、サポートされていない可能性があります。 たとえば、スプーラー EMF スプールが Windows 2000 以降のオペレーティング システム リリースし、「小冊子」オプションを無効になっている場合は、%pagepersheet 機能のサポートされていません。 別の例として、プリンターが Type42 ラスタライザーを持っていない場合、"NativeTrueType"オプションはサポートされていません %ttdownloadformat の。 これらのサポートされていないオプション EnumOptions の出力キーワードの一覧に表示されません。

Pscript は、特別な方法で、次の機能のキーワードを処理します。

-   \*CustomPageSize 機能キーワードは、このオプションに変換、 \*PageSize 機能キーワードでは、"CustomPageSize"オプションのキーワードをされているとします。 呼び出す**GetOptionAttribute**その PPD パラメーターを取得します。

-   \*ManualFeed True エントリは、このオプションに変換、 \*"ManualFeed"オプションのキーワード名の中で、InputSlot 機能キーワード。

-   \*InputSlot 機能キーワード、Pscript 常にオプションのキーワードの名前を持つドライバーが生成したオプションを追加します"\*UseFormTrayTable"最初のオプションとして (、"\*"プレフィックスを防ぐために、オプションのキーワード名で使用PPD 定義のオプションとの競合という名前)、これが、PPD. で定義されているオプションに続く 場合、"\*UseFormTrayTable"オプションを選択すると、Pscript は自動的に選択した用紙サイズをサポートする用紙トレイを選択する用紙トレイ割り当てテーブルを使用します。

 

 




