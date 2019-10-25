---
title: ドライバーへの作成通知とクローズ通知の不均衡の防止
description: ドライバーへの作成通知とクローズ通知の不均衡の防止
ms.assetid: e6678226-44d3-4b1d-a296-2017bc9c7c37
keywords:
- 作成-ファイル通知 WDK UMDF
- クリーンアップ-ファイル通知 WDK UMDF
- クローズファイル通知 WDK UMDF
- 通知 WDK UMDF
- 通知 WDK UMDF, 作成と終了の不均衡の防止
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de3fa6aef4ade16a26f2640a1d8eb576da3ddfac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842236"
---
# <a name="preventing-an-imbalance-of-create-and-close-notifications-to-a-driver"></a>ドライバーへの作成通知とクローズ通知の不均衡の防止


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

上位の UMDF ドライバーでは、 [**Iwdfdeviceinitialize:: AutoForwardCreateCleanupClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-autoforwardcreatecleanupclose)メソッドを使用して、フレームワークがデバイススタック内の次の下位のドライバーに対して、ファイルの作成、クリーンアップ、およびファイルの終了通知を自動的に転送するタイミングを制御できます. ただし、上位ドライバーは**AutoForwardCreateCleanupClose**をファイル単位ではなくデバイスレベルで自動的に転送するように設定するため、転送はデバイスのすべてのファイルで同じである必要があります。 このフレームワークにより、クリーンアップファイルとファイルのクローズ通知の転送動作が保証されます。 上位ドライバーが[**Iqueuecallbackcreate:: OnCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)コールバック関数を実装している場合、その転送動作がすべてのファイルの作成要求で同じであり、クリーンアップファイルの転送動作と一致していることを確認する必要があります。ファイルのクローズ通知。 そうしないと、ドライバーの**Iqueuecallbackcreate:: OnCreateFile**メソッドと[**IFileCallbackCleanup:: Oncleanupfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)メソッドと[**IFileCallbackClose:: onclosefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)メソッドの呼び出しが等しくない可能性があります。

下位のドライバーが大量の作成ファイルと閉じファイル通知を受信しないようにするには、上位ドライバーが[**Iqueuecallbackcreate:: OnCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)コールバック関数で次のことを確認する必要があります。

-   転送動作は、デバイスのすべてのファイルで同じです。

-   転送動作は、 [**Iwdfdeviceinitialize:: AutoForwardCreateCleanupClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-autoforwardcreatecleanupclose)の flag パラメーターを設定する方法と一致します。 それです：
    -   ドライバーがフラグを**Wdftrue**に設定した場合、ドライバーは、すべてのファイルの作成要求をデバイススタックから転送する必要があります。
    -   ドライバーがフラグを**WdfFalse**に設定している場合、ドライバーは、ファイルの作成要求をスタック内に転送しないようにする必要があります。
    -   ドライバーがフラグを**Wdfusedefault**とに設定した場合は、次のようになります。
        -   ドライバーが関数ドライバーの場合は、ファイルの作成要求をスタックに転送しないようにする必要があります。
        -   ドライバーがフィルタードライバーの場合は、すべての作成ファイル要求をスタックに転送する必要があります。

ドライバーがファイルの作成要求を転送できない場合でも、ドライバーは[**Iwdfdevice:: CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)メソッドを呼び出して新しい WDF ファイルを作成することにより、下位のドライバーに対する新しいファイルの作成要求を生成できます。 ドライバーは、新しく生成された作成ファイル要求の結果 (つまり、 **Createwdffile**の結果) に基づいて、元のファイル作成要求を完了できます。

 

 





