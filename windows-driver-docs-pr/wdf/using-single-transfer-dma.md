---
title: 単一転送 DMA の使用
description: このトピックでは、KMDF ドライバーがシングル転送 DMA を要求する方法について説明します。
ms.assetid: 57bf9988-6eed-42ca-a961-a6d16c5c19c1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c5988c3966a8d795ad2f9a6afcba1bc7fd270ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845437"
---
# <a name="using-single-transfer-dma"></a>単一転送 DMA の使用

既定では、WDF は1つの DMA トランザクションを複数の DMA 転送に分割することがあります。 ただし、一部のデバイスでは、フラグメント化されたトランザクションを処理できず、1つの DMA 操作ですべてのデータを受信する必要があります。  たとえば、一部の PCI ネットワークコントローラーには、部分的なデータをキャッシュおよび再組み立てするためのハードウェアがないため、一度に1つのネットワークパケットが必要です。

KMDF バージョン1.19 以降、DMA v3 を使用する KMDF ドライバーでは、シングル転送 DMA トランザクションが必要であることを指定できます。  ドライバーは、1つの DMA トランザクションに対して1つの転送のみを指定できます。または、指定した DMA イネーブラーを使用して作成されたすべての DMA トランザクションに対して1つの転送を指定できます。  

## <a name="setting-single-transfer-for-a-specific-dma-transaction"></a>特定の DMA トランザクションに対して1つの転送を設定する

1つのトランザクションに対してシングル転送を設定するには、次の順序を使用します。

1. [**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)または[**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)を呼び出します。
2. [**Wdfdmatransactionsetsingletransferrequirement 要件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)を呼び出します。
3. [**Wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)を呼び出します。  
    トランザクションの断片化によって初期化が失敗した場合、ドライバーは i/o 要求を失敗させるか、トランザクションのメモリバッファーを再配置してトランザクションを再初期化することができます。
4. [**Wdfdmatransactionexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)を呼び出します。

ドライバーをデバッグするときに、 [ **! wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)拡張機能を使用して、特定のトランザクションオブジェクトに対して単一転送が設定されているかどうかを確認できます。

## <a name="setting-the-single-transfer-requirement-for-all-dma-transactions-created-with-a-particular-dma-enabler"></a>特定の DMA イネーブラーで作成されたすべての DMA トランザクションに対して、単一転送の要件を設定する

特定のイネーブラーで作成されたすべてのトランザクションに対して単一転送を設定するには、 [**WdfDmaEnablerCreate**](https://docs.microsoft.com/previous-versions/jj619276(v=technet.10))を呼び出すときに[**WDF_DMA_ENABLER_CONFIG_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/ne-wdfdmaenabler-_wdf_dma_enabler_config_flags)に**WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**フラグを指定します。  

このフラグを使用するドライバーでは、トランザクションオブジェクトを作成または再利用するたびに、 [**Wdfdmatransactionsetsingletransferrequirement 要件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetsingletransferrequirement)を呼び出す必要はありません。

この設定は、ドライバーが[トランザクションオブジェクトを](reusing-dma-transaction-objects.md)再利用する場合にも保持されます。

デバッグ時には、 [ **! wdfkd. wdfdmaenabler**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)拡張機能を使用して、特定の DMA イネーブラーオブジェクトに対して単一転送が設定されているかどうかを確認します。

WDF がドライバーの DMA イベントコールバック関数を呼び出す順序の詳細については、「 [Bus マスタ Dma デバイス用の KMDF ドライバーでの I/o 要求の処理](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)」を参照してください。
