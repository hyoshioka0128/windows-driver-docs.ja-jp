---
title: ドライバーが作成したアプリケーションで作成されたファイル オブジェクトとの比較
description: ドライバーが作成したアプリケーションで作成されたファイル オブジェクトとの比較
ms.assetid: f81ae0ed-a29c-476e-9b16-ff554eef1de9
keywords:
- I/O WDK UMDF、ドライバーが作成を処理するために、ファイル オブジェクト
- アプリケーションで作成された、I/O の WDK UMDF を処理するために、ファイル オブジェクト
- I/O 要求 WDK の UMDF ドライバーが作成すると、ファイル オブジェクトのアプリケーションで作成されました。
- ユーザー モード ドライバー フレームワーク WDK、ハンドル I/O、ドライバーが作成したアプリケーションで作成されたとするファイル オブジェクト
- アプリケーションで作成されたとドライバー作成された UMDF WDK、I/O、処理するために、ファイル オブジェクト
- アプリケーションで作成されたとドライバー作成されたユーザー モード ドライバー WDK UMDF、I/O、処理するために、ファイル オブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b314aa2e8af9cd63c66a3dfd73ee327458d597b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550479"
---
# <a name="driver-created-versus-application-created-file-objects"></a>ドライバーが作成したアプリケーションで作成されたファイル オブジェクトとの比較


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

アプリケーションでは、デバイスを識別するハンドルが開いたら、フレームワークのドライバーの[ **IQueueCallbackCreate::OnCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff556841)メソッドへのポインターを提供し、 [ **IWDFFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558912)デバイスに関連付けられているファイル オブジェクトのインターフェイス。 アプリケーションは、開いているハンドルを送信するすべての I/O 要求は、作成されたファイル オブジェクトに関連付けられます。 フレームワークがドライバーによって提供されるのいずれかから適切なメソッドを呼び出すこのような要求が届いたら、 [UMDF キュー オブジェクト インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff561301)します。 ドライバーを呼び出して[ **IWDFIoRequest::GetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff559099)要求に関連付けられたファイル オブジェクトを決定します。 ドライバーを呼び出すことができます[ **AssignContext** ](https://msdn.microsoft.com/library/windows/hardware/ff560208) I/O セッションに固有のコンテキストに関連付けるファイル オブジェクト。

次の表は、アプリケーションは、呼び出しと、結果のドライバーが受信した通知を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アプリケーションを開始します</th>
<th align="left">ドライバーを受信します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Microsoft Win32 への呼び出し<a href="https://msdn.microsoft.com/library/windows/desktop/aa363858" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363858)"> <strong>CreateFile</strong> </a>関数。</p></td>
<td align="left"><p>呼び出しをその<a href="https://msdn.microsoft.com/library/windows/hardware/ff556841" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556841)"> <strong>IQueueCallbackCreate::OnCreateFile</strong> </a>メソッド。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Win32 呼び出し<strong>ReadFileEx</strong>、 <strong>WriteFileEx</strong>、または<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong> </a>関数。</p></td>
<td align="left"><p>呼び出しをその<a href="https://msdn.microsoft.com/library/windows/hardware/ff556875" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556875)"> <strong>IQueueCallbackRead::OnRead</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556885" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556885)"> <strong>IQueueCallbackWrite::OnWrite</strong></a>、または<a href="https://msdn.microsoft.com/library/windows/hardware/ff556854" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556854)"> <strong>IQueueCallbackDeviceIoControl::OnDeviceIoControl</strong> </a>メソッド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Win32 呼び出し<strong>CloseHandle</strong>ファイル オブジェクトへの最後の開いているハンドルの関数。</p></td>
<td align="left"><p>呼び出しをその<a href="https://msdn.microsoft.com/library/windows/hardware/ff554905" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554905)"> <strong>IFileCallbackCleanup::OnCleanupFile</strong> </a>メソッド。</p>
<p>ドライバーは、キャンセルまたはファイル オブジェクトに関連付けられているすべての I/O 要求を完了します。</p>
<p>クリーンアップの通知から返されると、ドライバー、UMDF は保留中の I/O 要求をキャンセルします。</p>
<p>ドライバーがへの呼び出しを受信したら、クリーンアップが完了して、保留中の I/O 要求がキャンセル UMDF、その<a href="https://msdn.microsoft.com/library/windows/hardware/ff554910" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554910)"> <strong>IFileCallbackClose::OnCloseFile</strong> </a>メソッド。</p></td>
</tr>
</tbody>
</table>

 

システム コンポーネントには、ユニバーサル Windows アプリの代わりの作成要求を発行可能性があります。 かどうかの作成を発行したアプリのプロセス ID を特定するドライバーのニーズを要求、呼び出すことができます、 [ **IWDFFile3::GetInitiatorProcessId** ](https://msdn.microsoft.com/library/windows/hardware/hh451279)メソッド。

## <a name="driver-created-file-objects"></a>ドライバーに作成されたファイル オブジェクト


ドライバーを作成し、I/O 要求の独立したを送信する必要がある場合 (既定 I/O ターゲット) ドライバー スタックの次のドライバーにアプリケーションを呼び出す必要があります[ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)にポインターを取得、 [ **IWDFDriverCreatedFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558895)インターフェイス。 この場合、[次へ] のドライバーは、アプリケーションが要求を生成するときに、ドライバーが受信する同じ通知を受信します。

次の表は、スタックで、ドライバーによって呼び出しと、結果の通知には、次のドライバーを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバーを開始します</th>
<th align="left">[次へ] のドライバー スタックを受信します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff558828" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateWdfFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558828)"> <strong>IWDFDevice::CreateWdfFile</strong> </a>メソッド。</p>
<p>UMDF が作成されたファイル オブジェクトは、デバイスと、スタックの次のデバイスの間の I/O セッションを表します。</p></td>
<td align="left"><p>呼び出しをその<a href="https://msdn.microsoft.com/library/windows/hardware/ff556841" data-raw-source="[&lt;strong&gt;IQueueCallbackCreate::OnCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556841)"> <strong>IQueueCallbackCreate::OnCreateFile</strong> </a>メソッド。</p></td>
</tr>
<tr class="even">
<td align="left"><p>呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557021" data-raw-source="[&lt;strong&gt;IWDFDevice::CreateRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557021)"> <strong>IWDFDevice::CreateRequest</strong> </a>メソッド。</p>
<p>要求の形式への呼び出し (への呼び出しなど、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559230" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559230)"> <strong>IWDFIoTarget::FormatRequestForIoctl</strong> </a>メソッド)。</p>
<p>呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559149" data-raw-source="[&lt;strong&gt;IWDFIoRequest::Send&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559149)"> <strong>IWDFIoRequest::Send</strong> </a>メソッド。</p></td>
<td align="left"><p>呼び出しをその<a href="https://msdn.microsoft.com/library/windows/hardware/ff556875" data-raw-source="[&lt;strong&gt;IQueueCallbackRead::OnRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556875)"> <strong>IQueueCallbackRead::OnRead</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556885" data-raw-source="[&lt;strong&gt;IQueueCallbackWrite::OnWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556885)"> <strong>IQueueCallbackWrite::OnWrite</strong></a>、または<a href="https://msdn.microsoft.com/library/windows/hardware/ff556854" data-raw-source="[&lt;strong&gt;IQueueCallbackDeviceIoControl::OnDeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556854)"> <strong>IQueueCallbackDeviceIoControl::OnDeviceIoControl</strong> </a>メソッド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff558897" data-raw-source="[&lt;strong&gt;IWDFDriverCreatedFile::Close&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558897)"> <strong>IWDFDriverCreatedFile::Close</strong> </a>メソッド。</p></td>
<td align="left"><p>呼び出しをその<a href="https://msdn.microsoft.com/library/windows/hardware/ff554905" data-raw-source="[&lt;strong&gt;IFileCallbackCleanup::OnCleanupFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554905)"> <strong>IFileCallbackCleanup::OnCleanupFile</strong> </a>メソッド。</p>
<p>ドライバーは、キャンセルまたはファイル オブジェクトに関連付けられているすべての I/O 要求を完了します。</p>
<p>クリーンアップの通知から返されると、ドライバー、UMDF は保留中の I/O 要求をキャンセルします。</p>
<p>ドライバーがへの呼び出しを受信したら、クリーンアップが完了して、保留中の I/O 要求がキャンセル UMDF、その<a href="https://msdn.microsoft.com/library/windows/hardware/ff554910" data-raw-source="[&lt;strong&gt;IFileCallbackClose::OnCloseFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554910)"> <strong>IFileCallbackClose::OnCloseFile</strong> </a>メソッド。</p></td>
</tr>
</tbody>
</table>

 

スタックの次のデバイスの違いが存在しない、アプリケーションによって作成されたファイル オブジェクトと上位層デバイスによって作成されるファイル オブジェクトの間。

 

 





