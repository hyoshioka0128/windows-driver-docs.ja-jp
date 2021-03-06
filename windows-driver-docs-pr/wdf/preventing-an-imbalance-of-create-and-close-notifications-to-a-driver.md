---
title: ドライバーへの作成通知とクローズ通知の不均衡の防止
description: ドライバーへの作成通知とクローズ通知の不均衡の防止
ms.assetid: e6678226-44d3-4b1d-a296-2017bc9c7c37
keywords:
- ファイルの作成通知 WDK UMDF
- クリーンアップ ファイル通知 WDK UMDF
- 閉じるファイル通知 WDK UMDF
- WDK UMDF の通知
- WDK UMDF、防止の通知が作成し、不均衡を閉じます
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 221296bb34ab2efec099813b7e2edb970b50631e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376332"
---
# <a name="preventing-an-imbalance-of-create-and-close-notifications-to-a-driver"></a>ドライバーへの作成通知とクローズ通知の不均衡の防止


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

上部の UMDF ドライバーを使用して、 [ **IWDFDeviceInitialize::AutoForwardCreateCleanupClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-autoforwardcreatecleanupclose)フレームワークが自動的に、ファイルの作成、クリーンアップ-ファイル、および閉じるファイルを転送場合を制御する方法デバイス スタックの次の下位のドライバーに通知します。 ただし、上のドライバーが設定されるため**AutoForwardCreateCleanupClose**およびファイルごとのレベルではなく、デバイス レベルでのみ自動的に転送する転送は、デバイスのすべてのファイルと同じことがあります。 フレームワークはこの転送クリーンアップ ファイルや閉じるファイル通知の動作により。 上のドライバーが実装されている場合、 [ **IQueueCallbackCreate::OnCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)コールバック関数にする必要があることを確認の転送動作が同じである要求で、一貫性のあるすべてのファイルを作成クリーンアップ ファイルや閉じるファイル通知の転送動作します。 そのために失敗する可能性が低いドライバーへの呼び出し数が等しくないを受信する、 **IQueueCallbackCreate::OnCreateFile**メソッドと[ **IFileCallbackCleanup::OnCleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)と[ **IFileCallbackClose::OnCloseFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)メソッド。

下位のドライバーが等しくない量のファイルを作成し、閉じるファイル通知を受信しないように、上のドライバーは、必ずでその[ **IQueueCallbackCreate::OnCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)コールバック関数それ：

-   その転送動作は、デバイスのすべてのファイルと同じです。

-   その転送動作のフラグ パラメーターを設定する方法と一致[ **IWDFDeviceInitialize::AutoForwardCreateCleanupClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-autoforwardcreatecleanupclose)します。 それです：
    -   ドライバーでは、フラグを設定場合**WdfTrue**ドライバーがデバイス スタックのすべてのファイルの作成要求を転送する必要があります。
    -   ドライバーでは、フラグを設定場合**WdfFalse**ドライバーは下位のスタックのファイルの作成要求のいずれかを転送しない必要があります。
    -   ドライバーでは、フラグを設定場合**WdfUseDefault**と。
        -   関数、ドライバーには、下位のスタックのすべてのファイルの作成要求を転送する必要があります。
        -   ドライバーが、フィルター ドライバーの場合は、下位のスタックのすべてのファイルの作成要求を転送する必要があります。

ドライバーがファイルの作成要求を転送できない場合、ドライバーによって引き続き下位のドライバーの新しいファイルの作成要求呼び出すことによって、 [ **IWDFDevice::CreateWdfFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)メソッドWDF の新しいファイルを作成します。 ドライバーは新しく生成された作成ファイル要求の結果に基づく元のファイルの作成要求を完了できます (つまりの結果から**CreateWdfFile**)。

 

 





