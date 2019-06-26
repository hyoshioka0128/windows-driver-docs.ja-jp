---
title: UMDF フィルター ドライバーのインストール
description: フィルター ドライバーでは、セットアップ クラスの特定のデバイスまたはすべてのデバイスをサポートできます。
ms.assetid: AE6D4E36-B758-451A-983E-6F0D7ADFD7A7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27c172a681a2cc9b8427487a8b6ba3bb19f96588
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371135"
---
# <a name="installing-a-umdf-filter-driver"></a>UMDF フィルター ドライバーのインストール


フィルター ドライバーでは、セットアップ クラスの特定のデバイスまたはすべてのデバイスをサポートできます。 上部のフィルターが関数デバイス上にアタッチ中に以下のデバイスの機能のドライバー、下位のフィルター ドライバーをアタッチします。

このトピックでは、インストールして、ユーザー モード ドライバー フレームワーク (UMDF) デバイスに固有の (上限または下限) フィルター ドライバーを構成する方法について説明します。 UMDF を使用して、クラス フィルター ドライバーを記述することはできません。 このトピックでは、両方の UMDF バージョン 1 と 2 に適用されます。

デバイス スタックを作成するときは、フレームワークは UMDF ドライバー スタックごとの 1 つだけの連続したブロック現在サポートしていることに留意してください。 また、同じデバイス スタックの UMDF バージョン 1 とバージョン 2 のドライバーをインストールすることはできません。

**インストールして、ドライバーを構成する方法**

1.  UMDF 1 フィルター ドライバーを呼び出す必要があります[ **IWDFDeviceInitialize::SetFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter)から、その[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数。 UMDF バージョン 2 以降、ドライバーはその代わりに呼び出す[ **WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitsetfilter)します。

2.  指定する必要がありますには、ドライバーを指定できます、UMDF 固有ディレクティブだけでなく、 **UmdfService**と**UmdfServiceOrder**ディレクティブ。 このトピックでは、上位のフィルター ドライバーを指定します。

    ```cpp
    [<mydriver>_Install.NT.Wdf]
    UmdfService=UMDFFunction,WUDFFuncDriver_Install
    UmdfService=UMDFFilter,UMDFFilter_Install
    UmdfServiceOrder=UMDFFunction,UMDFFilter
    ```

    ドライバーが記載されている順序でデバイス スタックに追加されます、 **UmdfServiceOrder**エントリ。 最初のパラメーターは、デバイス スタックの最下位の UMDF ドライバーを指定します。 下位のフィルター ドライバーをインストールするには、単純の引数を逆**UmdfServiceOrder**します。

    これらおよびその他の UMDF 固有 INF ディレクティブの詳細については、次を参照してください。 [INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)します。

3.  ドライバーのデバイスのスタックに UMDF ドライバーのみが含まれている場合は、この手順をスキップします。

    ドライバーのデバイスのスタックに UMDF ではないすべてのドライバーが含まれている場合、INF ファイルを含める必要があります、 **AddReg**セクション上部のフィルター ドライバーとして、reflector を指定します。

    ```cpp
    [<mydriver>_Device_AddReg]
    ; Load the redirector as an upperfilter on this specific device.
    ; 0x00010008 - FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
    HKR,,"UpperFilters",0x00010008,"WUDFRd" 
    ```

4.  上部のフィルターとして、ドライバーが読み込まれた後は、スタック内の次のドライバーへの I/O 要求を転送する責任を負います。 を示すためには、KMDF 関数ドライバー上にある単純なパススルー ドライバー (UMDF バージョン 1) を検討してください。

    最初に、既定の I/O のターゲットのインターフェイスを取得 (スタックの次のドライバー)。 書式を設定し、要求を送信します。 最も単純なシナリオは、次のようになります。

    ```cpp
    IWDFIoTarget * kmdfIoTarget = NULL;
        
        this->GetFxDevice()->GetDefaultIoTarget (&kmdfIoTarget);

        Request->FormatUsingCurrentType();

        hr = Request->Send (
            kmdfIoTarget, 
            0,  // 0 Submits Asynchronous else use WDF_REQUEST_SEND_OPTION_SYNCHRONOUS
            0);
    ```

 

 





