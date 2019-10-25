---
title: ドライバー作成ファイル オブジェクトとアプリケーション作成ファイル オブジェクトの比較
description: ドライバー作成ファイル オブジェクトとアプリケーション作成ファイル オブジェクトの比較
ms.assetid: f81ae0ed-a29c-476e-9b16-ff554eef1de9
keywords:
- i/o WDK UMDF を処理するファイルオブジェクト、ドライバー作成
- i/o WDK UMDF、アプリケーションで作成されたファイルオブジェクト
- I/o 要求 WDK UMDF、ファイルオブジェクト、ドライバー作成とアプリケーション作成
- ユーザーモードドライバーフレームワーク WDK、i/o を処理するためのファイルオブジェクト、ドライバーで作成されたものとアプリケーションで作成されたもの
- UMDF WDK、i/o を処理するためのファイルオブジェクト、ドライバーで作成されたものとアプリケーションで作成されたもの
- ユーザーモードドライバー WDK UMDF、i/o を処理するファイルオブジェクト、ドライバー作成とアプリケーション作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7bf13dbd1b5f1049894eb121499cc70a53389e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845593"
---
# <a name="driver-created-versus-application-created-file-objects"></a>ドライバー作成ファイル オブジェクトとアプリケーション作成ファイル オブジェクトの比較


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

アプリケーションがデバイスへのハンドルを開くと、フレームワークは、ドライバーの[**Iqueuecallbackcreate:: OnCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)メソッドを呼び出し、デバイスに関連付けられているファイルオブジェクトの[**Iwdffile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)インターフェイスへのポインターを提供します。 開いているハンドルにアプリケーションが送信する i/o 要求は、作成されたファイルオブジェクトに関連付けられます。 このような要求が到着すると、フレームワークは、ドライバーによって指定されたいずれかの[UMDF Queue オブジェクトインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/)から適切なメソッドを呼び出します。 次に、ドライバーは[**IWDFIoRequest:: GetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject)を呼び出して、要求に関連付けられているファイルオブジェクトを特定できます。 ドライバーは、ファイルオブジェクトに対して割り当て[**コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)を呼び出して、i/o セッションに固有のコンテキストを関連付けることができます。

次の表に、アプリケーションが行う呼び出しと、そのドライバーが受信する通知を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アプリケーションの開始</th>
<th align="left">ドライバーの受信</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Microsoft Win32 <a href="https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)"><strong>CreateFile</strong></a>関数の呼び出し。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)"><strong>Iqueuecallbackcreate:: OnCreateFile</strong></a>メソッドの呼び出し。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Win32 の<strong>ReadFileEx</strong>、<strong>た writefileex</strong>、または<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl</strong></a>関数の呼び出し。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread)"><strong>Iqueuecallbackread:: OnRead</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)"><strong>iqueuecallbackread:: onread</strong></a>、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)"><strong>IQueueCallbackDeviceIoControl:: OnDeviceIoControl</strong></a>メソッドの呼び出し。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ファイルオブジェクトへの最後に開いたハンドルに対する Win32 <strong>CloseHandle</strong>関数の呼び出し。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)"><strong>IFileCallbackCleanup:: OnCleanupFile</strong></a>メソッドの呼び出し。</p>
<p>ドライバーは、ファイルオブジェクトに関連付けられているすべての i/o 要求をキャンセルまたは完了します。</p>
<p>クリーンアップ通知からドライバーが戻った後、UMDF は保留中の i/o 要求をキャンセルします。</p>
<p>クリーンアップが完了し、UMDF が保留中の i/o 要求をキャンセルした後、ドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)"><strong>IFileCallbackClose:: OnCloseFile</strong></a>メソッドの呼び出しを受け取ります。</p></td>
</tr>
</tbody>
</table>

 

システムコンポーネントは、ユニバーサル Windows アプリの代わりに create 要求を発行する場合があります。 作成要求を発行したアプリのプロセス ID をドライバーが決定する必要がある場合は、 [**IWDFFile3:: GetInitiatorProcessId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffile3-getinitiatorprocessid)メソッドを呼び出すことができます。

## <a name="driver-created-file-objects"></a>ドライバーで作成されたファイルオブジェクト


ドライバーで、アプリケーションに依存しない i/o 要求をスタック内の次のドライバー (既定の i/o ターゲット) に作成して送信する必要がある場合、ドライバーは[**Iwdfdevice:: CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)を呼び出して[**Iwdfdriverのファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdrivercreatedfile)へのポインターを取得する必要があります。efi. この場合、次のドライバーは、アプリケーションが要求を生成するときに、ドライバーが受信するのと同じ通知を受け取ります。

次の表は、ドライバーが行う呼び出しと、スタック内の次のドライバーへの結果の通知を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーの開始</th>
<th align="left">スタック内の次のドライバーが受信する</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateWdfFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)"><strong>Iwdfdevice:: CreateWdfFile</strong></a>メソッドの呼び出し。</p>
<p>UMDF によって作成されるファイルオブジェクトは、デバイスとスタック内の次のデバイスとの間の i/o セッションを表します。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)"><strong>Iqueuecallbackcreate:: OnCreateFile</strong></a>メソッドの呼び出し。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)"><strong>Iwdfdevice:: CreateRequest</strong></a>メソッドの呼び出し。</p>
<p>要求を書式設定するための呼び出し (例: <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)"><strong>Iwdfiotarget:: FormatRequestForIoctl</strong></a>メソッドの呼び出し)。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)"><strong>IWDFIoRequest:: Send</strong></a>メソッドの呼び出し。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread)"><strong>Iqueuecallbackread:: OnRead</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)"><strong>iqueuecallbackread:: onread</strong></a>、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)"><strong>IQueueCallbackDeviceIoControl:: OnDeviceIoControl</strong></a>メソッドの呼び出し。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close" data-raw-source="[&lt;strong&gt;IWDFDriverCreatedFile::Close&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)"><strong>Iwdfdriverfile:: Close</strong></a>メソッドの呼び出し。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)"><strong>IFileCallbackCleanup:: OnCleanupFile</strong></a>メソッドの呼び出し。</p>
<p>ドライバーは、ファイルオブジェクトに関連付けられているすべての i/o 要求をキャンセルまたは完了します。</p>
<p>クリーンアップ通知からドライバーが戻った後、UMDF は保留中の i/o 要求をキャンセルします。</p>
<p>クリーンアップが完了し、UMDF が保留中の i/o 要求をキャンセルした後、ドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)"><strong>IFileCallbackClose:: OnCloseFile</strong></a>メソッドの呼び出しを受け取ります。</p></td>
</tr>
</tbody>
</table>

 

スタック内の次のデバイスでは、アプリケーションによって作成されたファイルオブジェクトと、それより上位のデバイスで作成されたファイルオブジェクトの間に違いはありません。

 

 





