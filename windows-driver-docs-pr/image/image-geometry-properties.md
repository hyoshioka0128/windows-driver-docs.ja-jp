---
title: イメージの Geometry プロパティ
description: イメージの Geometry プロパティ
ms.assetid: d1343ad4-3a54-414c-bc08-e07e0fb079cd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bafa66387e115d1c75bd05b8227aa8133edcf32a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352148"
---
# <a name="image-geometry-properties"></a>イメージの Geometry プロパティ





(ピマ 15740 標準を参照してください) ImgPixHeight と ImgPixWidth イメージ geometry のプロパティは、PTP では省略可能です。 これらのプロパティを実装しないカメラは、Microsoft PTP ミニドライバーは、全体のイメージをダウンロードし、これらのプロパティに適切な値を計算します。 これらの省略可能な PTP プロパティを実装することで発生してからこれを防ぐことができます。

 

 




