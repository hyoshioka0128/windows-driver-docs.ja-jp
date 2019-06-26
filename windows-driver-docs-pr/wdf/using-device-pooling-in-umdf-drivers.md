---
title: UMDF ドライバーでデバイス プールの使用
description: UMDF ドライバーでデバイス プールの使用
ms.assetid: EC36CB33-3877-445B-8AC6-1D41E6397FF9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5a6ec95511af4b74ce0ee4d6c444b22111691e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372271"
---
# <a name="using-device-pooling-in-umdf-drivers"></a>UMDF ドライバーでデバイス プールの使用


## <a name="user-mode-driver-framework-umdf-versions-111-and-20"></a>ユーザー モード ドライバー フレームワーク (UMDF) バージョン 1.11 および 2.0


ユーザー モード ドライバー フレームワーク (UMDF) ドライバーがビルドされたバージョン 1.11 または 2.0、Windows 8 以降を実行している場合は、フレームワークは、複数のデバイス スタックをホストできる Wudfhost の 1 つのインスタンスを作成します。 この手法と呼ばれる*デバイス プール*します。 デバイスのプールの主な利点は、UMDF デバイスが複数ある環境でのより少ないメモリ消費量です。

プールされているデバイスが失敗した場合、フレームワークは Wudfhost のインスタンスを終了し、すべてのプールに含まれていたデバイスの再起動を試みます。 場合は、デバイスは、プール間に再度失敗した、フレームワークは、デバイスの個別 Wudfhost プロセスを作成して、もう一度デバイスの起動を試みます。

別のホスト プロセスで、デバイスが失敗した場合、フレームワークは最大 5 回再起動しようとします。 フレームワークは、最後のエラーから 30 分が経過したときに、1 つにデバイスのエラー数をリセットします。

システムが再起動された場合は、別のプロセスで実行中に失敗したものを除くデバイスが repools フレームワーク。

デバイスが特定のデバイスのプールを無効にするには、 **UmdfHostProcessSharing** WDF 固有のディレクティブ*DDInstall* INF のセクション。 について**UmdfHostProcessSharing**を参照してください[INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)します。

ドライバーで使用する場合[ダイレクト I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)を設定する必要があります**UmdfHostProcessSharing**に**ProcessSharingDisabled**します。 それ以外の場合、ドライバーは、開始ができません。 場合**WdfDeviceIoBufferedOrDirect**が選択されているデバイスがプールされている、フレームワークは、バッファーにアクセスする方法を変更し、 [I/O バッファー](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)します。 場合**WdfDeviceIoBufferedOrDirect**が選択されていると、デバイスがプールされていない、フレームワークがダイレクト I/O をバッファーへのアクセス方法を変更します。

バッファーへのアクセス方法を選択するには、ドライバーを呼び出す必要があります、 [ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)メソッドからその[ **IDriverEntry::OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数。 アクセス方法については、次を参照してください。 [UMDF-Based ドライバーでのデータ バッファーへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)します。

## <a name="umdf-versions-19-and-earlier"></a>UMDF バージョン 1.9 以降


ドライバーが UMDF 1.9 またはそれ以前のバージョンでビルドされている場合、フレームワークは各デバイス スタックのホスト プロセス (Wudfhost) の個別のインスタンスを作成します。

デバイスは、開始に失敗した場合、フレームワークは、最大 5 回再起動しようとします。 フレームワークは、最後のエラーから 30 分が経過したときに、1 つにデバイスのエラー数をリセットします。

環境では、プールされていない、複数のデバイス スタックは同じ UMDF ドライバーを共有している場合。

-   各デバイス スタックは、別の WudfHost プロセスで読み込まれます。
-   フレームワークは、ドライバーの[ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)と[ **IDriverEntry::OnDeinitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)ごとに 1 回のメソッドデバイスのスタックです。
-   フレームワークは、ドライバーの[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)各デバイス スタックに対して 1 回のメソッド。 各デバイス オブジェクトは、個別のドライバー オブジェクトに関連付けられます。

環境では、プールされた、複数のデバイス スタックは、同じユーザー モード ドライバーを共有している場合。

-   各デバイス スタックは、同じ WudfHost プロセスで読み込まれます。
-   フレームワークは、ドライバーの[ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)と[ **IDriverEntry::OnDeinitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)メソッドを 1 回だけです。
-   フレームワークは、ドライバーの[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)各デバイス スタックに対して 1 回のメソッド。 各デバイス オブジェクトは、同じドライバー オブジェクトに関連付けられます。

プールされた構成で 1 つだけのドライバー オブジェクトがあるためは、グローバル変数またはドライバーのコールバック オブジェクトなど、デバイス間で共有されているオブジェクト、ドライバーはいない任意のデバイスごとのコンテキストを格納する必要があります。 代わりに、ドライバーは、ドライバーのデバイスのコールバック オブジェクトなど、デバイス スタック間で共有されていないオブジェクトでデバイスごとのコンテキストを格納する必要があります。

 

 





