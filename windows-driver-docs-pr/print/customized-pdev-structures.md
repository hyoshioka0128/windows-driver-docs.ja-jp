---
title: カスタマイズされた PDEV 構造体
description: カスタマイズされた PDEV 構造体
ms.assetid: e5c51b9a-5f73-4411-88d8-931981a8450c
keywords:
- プラグインを WDK の印刷、PDEV 構造の表示
- PDEV WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 819287a94b9decbd918cbf1dd7d857e850ac2269
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355698"
---
# <a name="customized-pdev-structures"></a>カスタマイズされた PDEV 構造体





レンダリングのプラグインでは、プライベート PDEV 構造をサポートするために 3 つのメソッドを実装します。 Unidrv レンダリング プラグインでは、次のメソッドを実装する必要があります。

[**IPrintOemUni::EnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff554249)

[**IPrintOemUni::DisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff554238)

[**IPrintOemUni::ResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff554270)

Pscript5 レンダリング プラグインでは、次のメソッドを実装する必要があります。

[**IPrintOemPS::EnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff553215)

[**IPrintOemPS::DisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff553209)

[**IPrintOemPS::ResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff553233)

PDEV 構造体には、総称です。 それを定義するモジュールで使用するためのプライベートなローカルに定義された構造体を指します。 通常、物理デバイスの特性を格納するために使用されます。 各プリンター ドライバーと各プラグインは、レンダリング PDEV 構造を定義します。 型"PDEV"のグローバルに定義された構造体はありません。

 

 




