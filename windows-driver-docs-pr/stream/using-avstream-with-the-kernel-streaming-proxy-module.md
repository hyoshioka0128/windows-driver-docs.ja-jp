---
title: カーネル ストリーミング プロキシ モジュールでの AVStream の使用
description: カーネル ストリーミング プロキシ モジュールでの AVStream の使用
ms.assetid: c8ae1385-337e-46ad-841e-fbdf5d685210
keywords:
- カーネル ストリーミング プロキシ WDK AVStream
- KS プロキシ WDK AVStream
- プロキシ ユーザー モード接続 WDK AVStream
- WDK AVStream メディアを種類します。
- DirectShow フィルター WDK AVStream
- AVStream カーネル ストリーミング プロキシ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a99a391a0b448b68f2d1f86c0b4130776572b9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367460"
---
# <a name="using-avstream-with-the-kernel-streaming-proxy-module"></a>カーネル ストリーミング プロキシ モジュールでの AVStream の使用





多くの場合、カーネル モードのフィルターがユーザー モードで接続されて、[カーネル ストリーミング プロキシ](https://msdn.microsoft.com/library/windows/hardware/ff560877)します。 このプロキシは、DirectShow フィルター モードをユーザーに表示されるカーネル モードのフィルターを使用します。

DirectShow が交差してフィルターを接続モードの接続を使用する場合、*メディアの種類*します。 これらのメディア タイプは、カーネル モードでのデータ形式に DirectShow 対応です。

DirectShow では、カーネル モードの暗証番号 (pin) のメディアの種類を列挙する場合は、暗証番号 (pin) のデータの範囲と、暗証番号 (pin) に対応するデータ範囲が交差するとします。 」の説明に従ってこの交差部分が、データ形式を生成[AVStream のデータ範囲の交差部分](data-range-intersections-in-avstream.md)します。 プロキシは、結果として得られるデータ形式を DirectShow メディアの種類に変換します。

カーネル モードのように、プロキシはメディアの種類が、許容されるか、メディアの種類が、pin でのデータ範囲の部分的な一致であるかどうかを判断するかどうかを判断するデータ ハンドラーかを確認します。 指定するには、カーネル モードのセマンティクス、主要な型、サブフォーマット、指定子のコンテキストでの部分的に一致することを示し、必要な属性と一致します。 メディアの種類が部分的に一致する場合は、接続が行われます。

AVStream にミニドライバーの呼び出し、接続が完了する前に、 [ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)設定されているデータ形式のミニドライバーを通知するためにディスパッチします。 この形式は、プロキシのピン留めするための提案がユーザー モードのメディアの種類に対応します。 AVStream には、形式については、部分的な一致するために決定されたデータ範囲も用意されています。

 

 




