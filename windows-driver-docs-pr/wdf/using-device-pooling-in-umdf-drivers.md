---
title: UMDF ドライバーでデバイス プールの使用
description: UMDF ドライバーでデバイス プールの使用
ms.assetid: EC36CB33-3877-445B-8AC6-1D41E6397FF9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 733197185e967f13821ce113115269a66297b861
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843088"
---
# <a name="using-device-pooling-in-umdf-drivers"></a>UMDF ドライバーでデバイス プールの使用


## <a name="user-mode-driver-framework-umdf-versions-111-and-20"></a>ユーザーモードドライバーフレームワーク (UMDF) バージョン1.11 および2.0


ユーザーモードドライバーフレームワーク (UMDF) ドライバーがバージョン1.11 または2.0 でビルドされ、Windows 8 以降で実行されている場合、フレームワークは、複数のデバイススタックをホストできる Wudfhost の1つのインスタンスを作成します。 この手法は、*デバイスプール*と呼ばれます。 デバイスプールの主な利点は、複数の UMDF デバイスがある環境でのメモリ消費量を削減することです。

プールされたデバイスで障害が発生した場合、フレームワークは Wudfhost のインスタンスを終了し、プール内にあったすべてのデバイスを再起動しようとします。 プールされている間にデバイスで障害が発生した場合、フレームワークはデバイス用に個別の Wudfhost プロセスを作成し、デバイスを再度起動しようとします。

デバイスが別のホストプロセスで失敗した場合、フレームワークは最大5回、再起動を試みます。 前回のエラーから30分が経過すると、デバイスのエラー数が1にリセットされます。

システムを再起動すると、別のプロセスで実行中にエラーが発生したデバイスを除き、フレームワークによってデバイスが再プールされます。

特定のデバイスのデバイスプールを無効にするには、INF の WDF 固有の*Ddinstall*セクションで**Umdfhostprocesssharing**ディレクティブを使用します。 **Umdfhostprocesssharing**の詳細については、「 [INF ファイルでの WDF ディレクティブの指定](specifying-wdf-directives-in-inf-files.md)」を参照してください。

ドライバーが[直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)を使用する場合は、 **Umdfhostprocesssharing**を**processsharingdisabled**に設定する必要があります。 そうしないと、ドライバーの起動に失敗する可能性があります。 **WdfDeviceIoBufferedOrDirect**が選択されていて、デバイスがプールされている場合、フレームワークはバッファーアクセスメソッドをバッファー [i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)に変更します。 **WdfDeviceIoBufferedOrDirect**が選択されていて、デバイスがプールされていない場合、フレームワークはバッファーアクセスメソッドをダイレクト i/o に変更します。

バッファーアクセスメソッドを選択するには、ドライバーで[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数から[**IWDFDeviceInitialize2:: SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)メソッドを呼び出す必要があります。 アクセスメソッドの詳細については、「 [UMDF ベースのドライバーでのデータバッファー](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers)へのアクセス」を参照してください。

## <a name="umdf-versions-19-and-earlier"></a>UMDF バージョン1.9 以前


ドライバーが UMDF version 1.9 またはそれ以前のバージョンでビルドされている場合、フレームワークは、デバイススタックごとにホストプロセス (Wudfhost) の個別のインスタンスを作成します。

デバイスの起動に失敗した場合、フレームワークは最大5回、再起動を試みます。 前回のエラーから30分が経過すると、デバイスのエラー数が1にリセットされます。

プールされていない環境で、複数のデバイススタックで同じ UMDF ドライバーが共有されている場合は、次のようになります。

-   各デバイススタックは、個別の WudfHost プロセスで読み込まれます。
-   フレームワークは、デバイススタックごとにドライバーの[**Idriverentry:: OnInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)メソッドと[**Idriverentry:: ondeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)メソッドを1回呼び出します。
-   フレームワークは、デバイススタックごとにドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドを1回呼び出します。 各デバイスオブジェクトは、個別のドライバーオブジェクトに関連付けられています。

プールされた環境で、複数のデバイススタックで同じユーザーモードドライバーが共有されている場合は、次のようになります。

-   各デバイススタックは、同じ WudfHost プロセスで読み込まれます。
-   フレームワークは、ドライバーの[**Idriverentry:: oninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)メソッドと[**Idriverentry:: ondeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeinitialize)メソッドを1回だけ呼び出します。
-   フレームワークは、デバイススタックごとにドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドを1回呼び出します。 各デバイスオブジェクトは、同じドライバーオブジェクトに関連付けられています。

プールされた構成にはドライバーオブジェクトが1つしかないため、ドライバーは、デバイスごとのコンテキストをグローバル変数に格納したり、ドライバーコールバックオブジェクトなど、デバイス間で共有されるオブジェクトに格納したりしないでください。 代わりに、ドライバーは、ドライバーのデバイスコールバックオブジェクトなど、デバイススタック間で共有されないオブジェクトにデバイスごとのコンテキストを格納する必要があります。

 

 





