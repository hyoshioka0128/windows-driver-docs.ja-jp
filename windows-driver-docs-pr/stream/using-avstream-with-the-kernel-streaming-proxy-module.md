---
title: カーネル ストリーミング プロキシ モジュールでの AVStream の使用
description: カーネル ストリーミング プロキシ モジュールでの AVStream の使用
ms.assetid: c8ae1385-337e-46ad-841e-fbdf5d685210
keywords:
- カーネルストリーミングプロキシ WDK AVStream
- KS プロキシ WDK AVStream
- プロキシユーザーモード接続 WDK AVStream
- メディアの種類 WDK AVStream
- DirectShow フィルター WDK AVStream
- AVStream カーネルストリーミングプロキシ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac2df22c14611ac2ab91b58ab36cf6c3bf042205
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842296"
---
# <a name="using-avstream-with-the-kernel-streaming-proxy-module"></a>カーネル ストリーミング プロキシ モジュールでの AVStream の使用





カーネルモードのフィルターは、多くの場合、ユーザーモードで[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)を介して接続されます。 このプロキシにより、DirectShow フィルターとしてユーザーモードにカーネルモードフィルターが表示されます。

このモードの接続を使用すると、DirectShow は、*メディアの種類*を交差させることによってフィルターを接続します。 これらのメディアの種類は、カーネルモードのデータ形式に対応する DirectShow です。

DirectShow がカーネルモードの pin でメディアの種類を列挙すると、ピンの対応するデータ範囲がピンのデータ範囲と交差します。 この積集合は、 [AVStream のデータ範囲の交差](data-range-intersections-in-avstream.md)部分で説明されているように、データ形式を生成します。 プロキシは、結果のデータ形式を DirectShow メディアタイプに変換します。

カーネルモードと同様に、プロキシは、メディアの種類が許容されるかどうかを判断するためにデータハンドラーに要求します。または、メディアの種類が pin のデータ範囲と部分的に一致しているかどうかを判断します。 部分一致は、カーネルモードセマンティクスのコンテキストで、メジャータイプ、サブフォーマット、指定子、および必須属性が一致することを示します。 メディアの種類が部分一致である場合は、接続が続行されます。

接続が完了する前に、AVStream はミニドライバーの[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)ディスパッチを呼び出して、設定されているデータ形式のミニドライバーを通知します。 この形式は、プロキシ化された pin に提示されたユーザーモードメディアの種類に対応しています。 AVStream では、形式の部分一致として決定されたデータ範囲も提供します。

 

 




