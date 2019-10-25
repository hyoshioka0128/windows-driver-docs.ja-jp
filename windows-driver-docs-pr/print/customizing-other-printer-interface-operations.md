---
title: その他のプリンター インターフェイスの操作をカスタマイズする
description: その他のプリンター インターフェイスの操作をカスタマイズする
ms.assetid: ae59d2e7-9049-432d-b519-9e7c88af8d48
keywords:
- ユーザーインターフェイスプラグイン WDK 印刷、カスタマイズ方法
- UI プラグイン WDK 印刷、カスタマイズ方法
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d26537426a3787eb4b698dfd39625fe6e7f421
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843374"
---
# <a name="customizing-other-printer-interface-operations"></a>その他のプリンター インターフェイスの操作をカスタマイズする





UI プラグインは、必要に応じて、次のいずれかの IPrintOemUI メソッドを実装できます。

[**IPrintOemUI::D eviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)

[**IPrintOemUI::D evQueryPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)

[**IPrintOemUI::P rinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-printerevent)

[**IPrintOemUI:: UpgradePrinter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)

これらのメソッドは、Unidrv および Pscript5 で使用されるユーザーモード[プリンターインターフェイス DLL](printer-interface-dll.md)によってエクスポートされる同様の名前付き関数と同じです。 これらのカスタマイズ方法では、ドライバーのプリンターインターフェイス DLL の同等の関数は置き換えられません。 どちらの場合も、最初に printer interface DLL 関数が呼び出され、次にドライバーがプラグインのカスタマイズメソッドを呼び出します。

 

 




