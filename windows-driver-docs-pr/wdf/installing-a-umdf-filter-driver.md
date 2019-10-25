---
title: UMDF フィルター ドライバーのインストール
description: フィルタードライバーは、セットアップクラスの特定のデバイスまたはすべてのデバイスをサポートできます。
ms.assetid: AE6D4E36-B758-451A-983E-6F0D7ADFD7A7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca50b91261b82f80968ba847dc90d8c7995cc8ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844771"
---
# <a name="installing-a-umdf-filter-driver"></a>UMDF フィルター ドライバーのインストール


フィルタードライバーは、セットアップクラスの特定のデバイスまたはすべてのデバイスをサポートできます。 下位のフィルタードライバーはデバイスの関数ドライバーの下にアタッチされ、上位のフィルターはデバイスの関数ドライバーの上にアタッチされます。

このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) デバイス固有 (アッパーまたは下位) のフィルタードライバーをインストールして構成する方法について説明します。 UMDF を使用してクラスフィルタードライバーを書き込むことはできません。 このトピックは、UMDF バージョン1と2の両方に適用されます。

デバイススタックを構築するときは、現在フレームワークでサポートされているのは、スタックごとに1つの UMDF ドライバーの連続したブロックのみであることに注意してください。 また、同じデバイススタックに、UMDF version 1 および version 2 のドライバーをインストールすることはできません。

**ドライバーをインストールして構成する方法**

1.  UMDF 1 フィルタードライバーは、 [**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数から[**Iwdfdeviceinitialize:: SetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter)を呼び出す必要があります。 UMDF バージョン2以降では、ドライバーは[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)を代わりに呼び出します。

2.  ドライバーで指定されているすべての UMDF 固有のディレクティブに加えて、 **umdfservice**と**Umdfserviceorder**ディレクティブを指定する必要があります。 このトピックでは、上位フィルタードライバーを指定します。

    ```cpp
    [<mydriver>_Install.NT.Wdf]
    UmdfService=UMDFFunction,WUDFFuncDriver_Install
    UmdfService=UMDFFilter,UMDFFilter_Install
    UmdfServiceOrder=UMDFFunction,UMDFFilter
    ```

    ドライバーは、 **Umdfserviceorder**エントリに記載されている順序でデバイススタックに追加されます。 最初のパラメーターは、デバイススタック内の最も下位の UMDF ドライバーを指定します。 下位のフィルタードライバーをインストールするには、 **Umdfserviceorder**の引数を逆にします。

    これらおよびその他の UMDF 固有の INF ディレクティブの詳細については、「 [Inf ファイルでの WDF ディレクティブの指定](specifying-wdf-directives-in-inf-files.md)」を参照してください。

3.  ドライバーのデバイススタックに UMDF ドライバーのみが含まれている場合は、この手順をスキップします。

    ドライバーのデバイススタックに、UMDF ではないドライバーが含まれている場合、INF ファイルには、リフレクターを上位フィルタードライバーとして指定する**AddReg**セクションが含まれている必要があります。

    ```cpp
    [<mydriver>_Device_AddReg]
    ; Load the redirector as an upperfilter on this specific device.
    ; 0x00010008 - FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
    HKR,,"UpperFilters",0x00010008,"WUDFRd" 
    ```

4.  ドライバーは、上位フィルターとして読み込まれた後、スタック内の次のドライバーに i/o 要求を転送します。 例として、KMDF 関数ドライバーを超える単純なパススルードライバー (UMDF version 1) について考えてみましょう。

    まず、既定の i/o ターゲット (スタック内の次のドライバー) のインターフェイスを取得します。 次に、要求を書式設定して送信します。 最も単純なシナリオは次のようになります。

    ```cpp
    IWDFIoTarget * kmdfIoTarget = NULL;
        
        this->GetFxDevice()->GetDefaultIoTarget (&kmdfIoTarget);

        Request->FormatUsingCurrentType();

        hr = Request->Send (
            kmdfIoTarget, 
            0,  // 0 Submits Asynchronous else use WDF_REQUEST_SEND_OPTION_SYNCHRONOUS
            0);
    ```

 

 





