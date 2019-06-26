---
title: カスタマイズされた PDEV 構造体
description: カスタマイズされた PDEV 構造体
ms.assetid: e5c51b9a-5f73-4411-88d8-931981a8450c
keywords:
- プラグインを WDK の印刷、PDEV 構造の表示
- PDEV WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7166e081757ccc3a8a64ed68da23ce39bf2451c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372387"
---
# <a name="customized-pdev-structures"></a>カスタマイズされた PDEV 構造体





レンダリングのプラグインでは、プライベート PDEV 構造をサポートするために 3 つのメソッドを実装します。 Unidrv レンダリング プラグインでは、次のメソッドを実装する必要があります。

[**IPrintOemUni::EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)

[**IPrintOemUni::DisablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-disablepdev)

[**IPrintOemUni::ResetPDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-resetpdev)

Pscript5 レンダリング プラグインでは、次のメソッドを実装する必要があります。

[**IPrintOemPS::EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enablepdev)

[**IPrintOemPS::DisablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-disablepdev)

[**IPrintOemPS::ResetPDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-resetpdev)

PDEV 構造体には、総称です。 それを定義するモジュールで使用するためのプライベートなローカルに定義された構造体を指します。 通常、物理デバイスの特性を格納するために使用されます。 各プリンター ドライバーと各プラグインは、レンダリング PDEV 構造を定義します。 型"PDEV"のグローバルに定義された構造体はありません。

 

 




