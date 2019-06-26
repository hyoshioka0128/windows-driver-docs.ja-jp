---
title: その他のプリンター インターフェイスの操作をカスタマイズする
description: その他のプリンター インターフェイスの操作をカスタマイズする
ms.assetid: ae59d2e7-9049-432d-b519-9e7c88af8d48
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、カスタマイズ メソッド
- UI プラグインの WDK 印刷、カスタマイズ方法
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d846f697fb05ad7d73e5aa0949be2b5d97d736
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372386"
---
# <a name="customizing-other-printer-interface-operations"></a>その他のプリンター インターフェイスの操作をカスタマイズする





プラグインの UI は、必要に応じて次 IPrintOemUI メソッドのいずれかに実装できます。

[**IPrintOemUI::DeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)

[**IPrintOemUI::DevQueryPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)

[**IPrintOemUI::PrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-printerevent)

[**IPrintOemUI::UpgradePrinter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)

メソッドは、同様に、ユーザー モードでエクスポートされた名前付きの関数に相当[プリンター インターフェイス DLL](printer-interface-dll.md) Unidrv と Pscript5 によって使用されます。 これらのカスタマイズの方法では、ドライバーのプリンター インターフェイス DLL で同等の関数は置き換えられません。 各ケースでプリンター インターフェイス DLL 関数が最初に呼び出されないし、ドライバーがプラグのカスタマイズ メソッドを呼び出します。

 

 




