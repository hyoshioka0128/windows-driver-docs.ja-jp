---
title: Unidrv と PScript5 の印刷ドライバーの印刷機能
description: Unidrv と PScript5 の印刷ドライバーの印刷機能
ms.assetid: 70f8b846-3e05-4345-baad-a3db6b8df620
keywords:
- 印刷機能、WDK Unidrv
- 印刷機能、WDK PScript5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2dbbfd665cd526b364151d49d1c1cf0edb20e56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373778"
---
# <a name="print-capabilities-in-unidrv-and-pscript5-print-drivers"></a>Unidrv と PScript5 の印刷ドライバーの印刷機能


Unidrv と PScript5 ミニドライバーは、印刷機能の機能をサポートするために必要な印刷チケットと印刷機能のインターフェイスを提供します。 これらのプリンター ドライバーは、印刷チケットを提供し、印刷機能が記載されている機能のサポート、[説明 (GPD) ファイルの一般的なプリンター](introduction-to-gpd-files.md)または PostScript プリンター説明 (PPD) ファイルを必要に応じて、かどうか機能に関する情報がパブリックまたはプライベートの部分では、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体。

[XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md)両方、GDI ベースのプリンター構成インターフェイスに必要なサポートを提供する Unidrv プリンターの構成 DLL を使用してもでき、 [IPrintTicketProvider インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))します。 Unidrv 構成 DLL を使用する場合は、basic 機能プリンターを XPSDrv プリンター ドライバーの開発を高速化できますかパススルー印刷ドライバー。

 

 




