---
title: KMDF ドライバーでの DMA のテスト
description: KMDF ドライバーでの DMA のテスト
ms.assetid: 1D37F8B3-EAFC-4BB0-988D-64ADF30DBC40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c1f02897021ee80b3c3bea917968efda609303e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350636"
---
# <a name="testing-dma-in-kmdf-drivers"></a>KMDF ドライバーでの DMA のテスト


\[KMDF にのみ適用されます。\]

次のツールは、DMA をサポートするフレームワーク ベースのドライバーをデバッグできます。

-   [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448) DMA のさまざまな操作の不適切な使用を検出する特定の検証テストが含まれています。 DMA 固有の検証の詳細については、次を参照してください。 [DMA の検証](https://msdn.microsoft.com/library/windows/hardware/ff544915)です。

-   [ **! Dma** ](https://msdn.microsoft.com/library/windows/hardware/ff562369)カーネル デバッガー拡張機能は、DMA サブシステムとにより検証される DMA デバイス ドライバーに関する情報を表示[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)します。

-   [カーネル モード ドライバー フレームワークの拡張機能](https://msdn.microsoft.com/library/windows/hardware/ff551876)DMA 固有の次のコマンドが含まれます。

    <a href="" id="-wdfcommonbuffer"></a>[**! wdfcommonbuffer**](https://msdn.microsoft.com/library/windows/hardware/ff565679)  
    一般的なバッファーの指定したオブジェクトに関する情報をダンプします。

    <a href="" id="-wdfdmaenabler"></a>[**!wdfdmaenabler**](https://msdn.microsoft.com/library/windows/hardware/ff565717)  
    DMA イネーブラーの特定のオブジェクトとそのトランザクションおよび共通のバッファー オブジェクトに関する情報をダンプします。

    <a href="" id="-wdfdmaenablers"></a>[**! wdfdmaenablers**](https://msdn.microsoft.com/library/windows/hardware/ff565719)  
    DMA イネーブラー、トランザクション、および共通のバッファー オブジェクトのすべての一覧を表示します。

    <a href="" id="-wdfdmatransaction"></a>[**! wdfdmatransaction**](https://msdn.microsoft.com/library/windows/hardware/ff565721)  
    特定のトランザクション オブジェクトに関する情報をダンプします。

 

 





