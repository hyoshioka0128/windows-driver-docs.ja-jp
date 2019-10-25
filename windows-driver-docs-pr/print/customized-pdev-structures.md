---
title: カスタマイズされた PDEV 構造体
description: カスタマイズされた PDEV 構造体
ms.assetid: e5c51b9a-5f73-4411-88d8-931981a8450c
keywords:
- プラグイン WDK print、PDEV 構造体のレンダリング
- PDEV WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a70e9937d1d1ffef506ddcfaaefb4ae6291c6911
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843379"
---
# <a name="customized-pdev-structures"></a>カスタマイズされた PDEV 構造体





レンダリングプラグインは、プライベート PDEV 構造体をサポートする3つのメソッドを実装します。 Unidrv レンダリングプラグインは、次のメソッドを実装する必要があります。

[**IPrintOemUni:: EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)

[**IPrintOemUni::D isablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disablepdev)

[**IPrintOemUni:: ResetPDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-resetpdev)

Pscript5 レンダリングプラグインには、次のメソッドを実装する必要があります。

[**IPrintOemPS:: EnablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)

[**IPrintOemPS::D isablePDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-disablepdev)

[**IPrintOemPS:: ResetPDEV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-resetpdev)

PDEV 構造体は汎用的な用語です。 これは、それを定義するモジュールによって使用される、プライベートなローカルに定義された構造体を参照します。 通常は、物理デバイスの特性を格納するために使用されます。 各プリンタードライバーと各レンダリングプラグインによって、独自の PDEV 構造が定義されます。 "PDEV" 型のグローバルに定義された構造がありません。

 

 




