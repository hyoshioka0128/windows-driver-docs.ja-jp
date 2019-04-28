---
title: WIA 項目を使用する WIA デバイスの記述
description: WIA 項目を使用する WIA デバイスの記述
ms.assetid: d8149f78-e095-48f9-be79-ff115b25f14e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df21a7249de123b39cb2a049a697ae09143be51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373206"
---
# <a name="describing-a-wia-device-using-wia-items"></a>WIA 項目を使用する WIA デバイスの記述





このトピックには、Windows Vista 以降が適用されます。

WIA 項目は、WIA デバイス (たとえば、スキャナーの自動ドキュメント フィーダー) またはそのデバイス (たとえば、カメラで画像) で格納されているデータのプログラミング可能なデータ ソースを表すことができます。 WIA デバイスは、そのデバイスによって生成されたさまざまなデータを正確に説明する項目を個別に分割する必要があります。 2 つの例を次に示します。

<a href="" id="scanner-example"></a>**スキャナーの例**  
フラット ベッドのスキャンとドキュメント フィーダー付きのスキャンの両方をサポートする WIA スキャナー デバイスでは、2 つの主要な子項目があります。 1 つの子項目はスキャン機能では、フラット ベッドを表し、他のスキャン機能ドキュメント フィーダーを表します。

<a href="" id="camera-example"></a>**カメラの使用例**  
画像を格納する WIA カメラ デバイスには、サブフォルダーおよび画像を表す子項目があります。

このセクションの残りの部分には、次のトピックが含まれています。

[WIA 項目のフラグ](wia-item-flags.md)

[WIA 項目のカテゴリ](wia-item-categories.md)

[WIA 項目のフラグとカテゴリの使用例](example-usage-of-wia-item-flags-and-categories.md)

[WIA ルート項目](wia-root-item.md)

[WIA データ項目](wia-data-item.md)

 

 




