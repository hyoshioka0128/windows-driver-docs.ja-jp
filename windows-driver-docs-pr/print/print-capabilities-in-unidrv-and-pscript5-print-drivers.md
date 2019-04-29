---
title: Unidrv と PScript5 の印刷ドライバーの印刷機能
description: Unidrv と PScript5 の印刷ドライバーの印刷機能
ms.assetid: 70f8b846-3e05-4345-baad-a3db6b8df620
keywords:
- 印刷機能、WDK Unidrv
- 印刷機能、WDK PScript5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327886f212ca8e6ec85a6da22098bd8c8c24024a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389486"
---
# <a name="print-capabilities-in-unidrv-and-pscript5-print-drivers"></a>Unidrv と PScript5 の印刷ドライバーの印刷機能


Unidrv と PScript5 ミニドライバーは、印刷機能の機能をサポートするために必要な印刷チケットと印刷機能のインターフェイスを提供します。 これらのプリンター ドライバーは、印刷チケットを提供し、印刷機能が記載されている機能のサポート、[説明 (GPD) ファイルの一般的なプリンター](introduction-to-gpd-files.md)または PostScript プリンター説明 (PPD) ファイルを必要に応じて、かどうか機能に関する情報がパブリックまたはプライベートの部分では、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体。

[XPSDrv プリンター ドライバー](xpsdrv-printer-drivers.md)両方、GDI ベースのプリンター構成インターフェイスに必要なサポートを提供する Unidrv プリンターの構成 DLL を使用してもでき、 [IPrintTicketProvider インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff554375)します。 Unidrv 構成 DLL を使用する場合は、basic 機能プリンターを XPSDrv プリンター ドライバーの開発を高速化できますかパススルー印刷ドライバー。

 

 




