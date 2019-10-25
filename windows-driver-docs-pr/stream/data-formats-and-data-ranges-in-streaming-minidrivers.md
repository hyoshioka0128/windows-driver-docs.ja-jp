---
title: ストリーミング ミニドライバーのデータ形式とデータ範囲
description: ストリーミング ミニドライバーのデータ形式とデータ範囲
ms.assetid: ea3aa4af-0c8c-429e-b399-0a196eadc5ef
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、データ形式、および範囲
- streaming ミニドライバー WDK Windows 2000 カーネル、データ形式、および範囲
- ミニドライバー WDK Windows 2000 カーネルストリーミング、データ形式、および範囲
- データ形式 WDK streaming ミニドライバー
- データ範囲 WDK streaming ミニドライバー
- 範囲 WDK streaming ミニドライバー
- WDK streaming ミニドライバーの形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d901b623cc92394202f46f852c75ddbb6763c162
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845148"
---
# <a name="data-formats-and-data-ranges-in-streaming-minidrivers"></a>ストリーミング ミニドライバーのデータ形式とデータ範囲





各ストリームは、その[**HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)構造の**StreamFormatsArray**メンバーでサポートされるデータ範囲を詳細に説明します。

形式と範囲の積集合の詳細については、「 [AVStream のデータ範囲の交差](data-range-intersections-in-avstream.md)部分」を参照してください。

 

 




