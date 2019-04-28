---
title: イメージへの添付ファイルの追加
description: イメージへの添付ファイルの追加
ms.assetid: 704f541b-b98c-44a8-bb19-5d5d0d1eab78
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8946c0775106ea6b0436b767a4cdcc0acf629b31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367119"
---
# <a name="adding-attachments-to-images"></a>イメージへの添付ファイルの追加





項目がマークされている場合**WiaItemTypeHasAttachments**、つまり、項目に子項目として格納されている添付ファイルが関連付けられていること。 型の項目と同じです。 これはいない**WiaItemTypeFolder**します。 主な相違点は次のとおりです。

-   アイテムの種類**WiaItemTypeHasAttachments**子のレベルが 1 つだけです。 アイテムの種類**WiaItemTypeFolder**レベルの子の任意の数を持つことができます。

-   型の項目のすべての子**WiaItemTypeHasAttachments**その項目に関連します。 たとえば、画像アイテムには、オーディオ データが関連付けられているが場合、画像アイテムの子としてオーディオのデータが格納され、画像アイテムが付きます**WiaItemTypeHasAttachments**します。

項目は型の両方にすることはできません**WiaItemTypeHasAttachments**と種類**WiaItemTypeFolder**します。 ただし、型の項目は、 **WiaItemTypeHasAttachments**と種類**WiaItemTypeFile**します。 これは、ため、項目の種類の**WiaItemTypeHasAttachments**は、概念的には、単一のエンティティとして扱われます。 次の図は、添付ファイル付き WIA カメラ項目のツリーを示しています。

![wia カメラ項目ツリーの添付ファイルを示す図](images/camera-tree-attachments.png)

 

 




