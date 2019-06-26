---
title: KMDF ドライバーでの DMA のテスト
description: KMDF ドライバーでの DMA のテスト
ms.assetid: 1D37F8B3-EAFC-4BB0-988D-64ADF30DBC40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b65bcead90da7d014fab74eae5b6b66b3046f79
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372317"
---
# <a name="testing-dma-in-kmdf-drivers"></a>KMDF ドライバーでの DMA のテスト


\[KMDF にのみ適用されます。\]

次のツールは、DMA をサポートするフレームワーク ベースのドライバーをデバッグできます。

-   [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier) DMA のさまざまな操作の不適切な使用を検出する特定の検証テストが含まれています。 DMA 固有の検証の詳細については、次を参照してください。 [DMA の検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/dma-verification)です。

-   [ **! Dma** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-dma)カーネル デバッガー拡張機能は、DMA サブシステムとにより検証される DMA デバイス ドライバーに関する情報を表示[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。

-   [カーネル モード ドライバー フレームワークの拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)DMA 固有の次のコマンドが含まれます。

    <a href="" id="-wdfcommonbuffer"></a>[ **! wdfcommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcommonbuffer)  
    一般的なバッファーの指定したオブジェクトに関する情報をダンプします。

    <a href="" id="-wdfdmaenabler"></a>[ **!wdfdmaenabler**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)  
    DMA イネーブラーの特定のオブジェクトとそのトランザクションおよび共通のバッファー オブジェクトに関する情報をダンプします。

    <a href="" id="-wdfdmaenablers"></a>[ **! wdfdmaenablers**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenablers)  
    DMA イネーブラー、トランザクション、および共通のバッファー オブジェクトのすべての一覧を表示します。

    <a href="" id="-wdfdmatransaction"></a>[ **! wdfdmatransaction**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)  
    特定のトランザクション オブジェクトに関する情報をダンプします。

 

 





