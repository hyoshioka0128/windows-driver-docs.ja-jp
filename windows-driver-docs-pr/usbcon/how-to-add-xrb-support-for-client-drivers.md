---
Description: このトピックでは、USB クライアントドライバーが Windows Driver Model (WDM) ドライバールーチンを使用して、Microsoft 提供の USB ドライバースタックに要求を送信する前に、URB の割り当てとフォーマットを行う方法について説明します。
title: URB の割り当てと構築
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936cae4b8e442700432ea58b487b813342922f90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844995"
---
# <a name="allocating-and-building-urbs"></a>URB の割り当てと構築

USB クライアントドライバーは、Windows Driver Model (WDM) ドライバールーチンを使用して、Microsoft が提供する USB ドライバースタックに要求を送信する前に、URB の割り当てとフォーマットを行うことができます。

クライアントドライバーは、URB を使用して、USB ドライバースタック内の下位のドライバーが要求を処理するために必要なすべての情報をパッケージ化します。 Windows オペレーティングシステムでは、urb は[**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造に記述されています。

Microsoft は、 [USB クライアントドライバー用のルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#client)のライブラリを提供しています。 これらのルーチンを使用することにより、USB クライアントドライバーは特定の指定された操作に対して URB 要求を作成し、USB スタックに転送できます。 必要に応じて、独自の URB 要求を作成するのではなく、サポートされている操作に対してライブラリルーチンを呼び出すようにクライアントドライバーを設計できます。

## <a name="urb-allocation-in-windows7-and-earlier"></a>Windows 7 以前での URB 割り当て

Windows 7 以前のバージョンの windows 用 Windows Driver Kit (WDK) に含まれるルーチンを使用して USB 要求を送信するために、クライアントドライバーは通常、 [**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造を割り当てて入力し、 **urb**構造を新しい IRP に関連付け、irp を送信します。を USB ドライバースタックにします。

Microsoft は、特定の種類の要求に対して、 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造の割り当てと書式設定を行うヘルパールーチン (Usbd によってエクスポートされる) を提供します。 たとえば、 [**USBD\_CreateConfigurationRequestEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)ルーチンは、 **urb**構造にメモリを割り当て、選択構成要求の urb を設定して、クライアントドライバーに**urb**構造体のアドレスを返します。 ただし、ヘルパールーチンは、すべての種類の要求に対して使用することはできません。

Microsoft では、一部の種類の要求に対して URBs という形式のマクロも提供しています。 これらのマクロの場合、クライアントドライバーは、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出すか、スタックに構造体を割り当てることによって、 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体を割り当てる必要があります。 たとえば、クライアントドライバーが**urb**を割り当てると、ドライバーは[**Usbbuildselectconfigurationrequest**](https://docs.microsoft.com/previous-versions/ff538968(v=vs.85))を呼び出して、選択構成要求の urb をフォーマットしたり、構成をクリアしたりできます。

その他の要求については、クライアントドライバーは、要求の種類に応じて、 [**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体のさまざまなメンバーを設定して、手動で urb の割り当てとフォーマットを行う必要があります。

USB 要求が完了すると、クライアントドライバーは[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造を解放する必要があります。 URB がスタックに割り当てられている場合、URB はスコープ外に出ると解放されます。 URB が非ページプールで割り当てられている場合、クライアントドライバーは、URB を解放するために[**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出す必要があります。

## <a name="urb-allocation-in-windows8"></a>Windows 8 での URB 割り当て

Windows 8 用 WDK は、URBs を割り当て、書式設定、および解放するためのルーチンをエクスポートする新しいスタティックライブラリ (Usbdex .lib) を提供します。 また、URB を IRP に関連付ける新しい方法があります。 新しいルーチンは、Windows Vista 以降のバージョンの Windows を対象とするクライアントドライバーから呼び出すことができます。

Windows Vista 以降で実行されているクライアントドライバーは、基になる USB ドライバースタックで特定のパフォーマンスと信頼性の向上を利用できるように、新しいルーチンを使用する必要があります。 これらの機能強化は、USB 3.0 デバイスとホストコントローラーをサポートするために Windows 8 で導入された新しい USB ドライバースタックに適用されます。 USB 2.0 ホストコントローラーの場合、Windows は、機能強化をサポートしていない以前のバージョンのドライバースタックを読み込みます。 基になるドライバースタックのバージョンや、ホストコントローラーでサポートされているプロトコルのバージョンに関係なく、常に新しい URB ルーチンを呼び出す必要があります。

新しいルーチンを呼び出す前に、クライアントドライバーを USB ドライバースタックに登録するための USBD ハンドルがあることを確認してください。 USBD ハンドルを取得するには、 [**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)を呼び出します。

次のルーチンは、Windows 8 の WDK で使用できます。 これらのルーチンは、Usbdlib .h で定義されています。

* [**USBD\_Ur・検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)
* [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)
* [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
* [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
* [**USBD\_UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)
* [**USBD\_割り当て Urbtoiostacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)

前の一覧の割り当てルーチンは、USB ドライバースタックによって割り当てられた新しい[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体へのポインターを返します。 Windows によって読み込まれた USB ドライバースタックのバージョンによっては、 **urb**構造を不透明な*urb コンテキスト*と組み合わせることができます。 URB コンテキストは、URB に関する情報のブロックです。 URB ヘッダーの内容を表示することはできません。この情報は、USB ドライバースタックによって内部的に使用され、URB の追跡と処理を改善するためのものです。 URB コンテキストは、Windows 8 の USB ドライバースタックで*のみ*使用されます。
URB コンテキストが使用可能な場合は、USB ドライバースタックによって、URB 処理がより安全で効率的になるように使用されます。 たとえば、USB ドライバースタックでは、クライアントドライバーが URB を送信せず、最初の要求が完了する前に同じ URB を再利用しようとしたことを確認する必要があります。 この種のエラーを検出するために、USB ドライバースタックは、状態情報を URB コンテキストに格納します。 状態情報がない場合、USB ドライバースタックは、受信した URB と現在進行中のすべての URBs を比較する必要があります。 状態情報は、クライアントドライバーが URB を解放しようとしたときに、USB ドライバースタックによっても使用されます。 URB を解放する前に、USB ドライバースタックは、URB が保留されていないことを確認するために状態を検証します。

URB コンテキストは、追加の URB 情報を格納するための公式なメカニズムを提供します。 必要に応じて追加のメモリを割り当てる場合や、 [**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体の予約されたメンバーに追加情報を格納する場合は、urb コンテキストを使用することをお勧めします。 USB ドライバースタックは、URBs とそれに関連付けられている URB コンテキストを非ページプールに割り当てます。そのため、将来的には、より大きな URB コンテキストが必要な場合に、必要な調整はプール割り当てのサイズのみになります。

## <a name="urb-routine-migration"></a>URB 定期移行

次の表は、URB ルーチンの変更点をまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ユースケース</th>
<th>Windows 7 以前の WDK で使用可能</th>
<th>Windows 8 用 WDK で利用可能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td>Windows 7 以前のバージョンのオペレーティングシステムを対象とする</td>
<td>Windows Vista 以降のバージョンのオペレーティングシステムを対象とします。</td>
</tr>
<tr class="even">
<td>URB を作成するには...</td>
<td>クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>構造体を割り当て、要求に応じて構造の形式を設定します。
<p>クライアントドライバーは、スタックに URB 構造体を割り当てます。または、ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>Exallocatepoolwithtag</strong></a>を呼び出して、非ページプールに構造体を割り当てます。</p></td>
<td>クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate" data-raw-source="[&lt;strong&gt;USBD_UrbAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)"><strong>USBD_UrbAllocate</strong></a>を呼び出し、新しい<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>構造体へのポインターを受け取ります。これは、USB ドライバースタックによって割り当てられます。 基になる USB ドライバースタックの USBD インターフェイスバージョンによっては、URB が URB コンテキストに関連付けられている場合があります。</td>
</tr>
<tr class="odd">
<td>構成の選択要求の URB を作成するには...</td>
<td>クライアントドライバーは、USB ドライバースタックによって作成およびフォーマットされた新しい URB へのポインターを返す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex" data-raw-source="[&lt;strong&gt;USBD_CreateConfigurationRequestEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)"><strong>USBD_CreateConfigurationRequestEx</strong></a>ルーチンを呼び出します。</td>
<td>クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a>を呼び出し、新しい<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>構造体へのポインターを受け取ります。この構造は、USB ドライバースタックによって割り当てられ、フォーマットされています (選択構成要求の場合)。 基になる USB ドライバースタックの USBD インターフェイスバージョンによっては、URB が URB コンテキストに関連付けられている場合があります。</td>
</tr>
<tr class="even">
<td>選択インターフェイス要求の URB を作成するには...</td>
<td>クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>構造体を割り当て、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface)"><strong>_URB_SELECT_INTERFACE</strong></a>構造体を使用して、USB デバイスの SELECT INTERFACE コマンドの形式を定義します。</td>
<td>クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a>を呼び出し、新しい<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>構造体へのポインターを受け取ります。これは、USB ドライバースタックによって割り当てられ、(選択インターフェイスの要求のために) 書式設定されます。 基になる USB ドライバースタックの USBD インターフェイスバージョンによっては、URB が URB コンテキストに関連付けられている場合があります。</td>
</tr>
<tr class="odd">
<td>URB を IRP に関連付けるには...</td>
<td>クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)"><strong>Iogetnextiシャー</strong></a>ドの場所を呼び出すことによって、次の IRP スタック位置へのポインターを取得します。 次に、クライアントドライバーは、スタック位置の<strong>引数 1</strong>メンバーを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>構造体のアドレスに手動で設定します。</td>
<td>クライアントドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)"><strong>Iogetnextiシャー</strong></a>ドの場所を呼び出すことによって、次の IRP スタック位置へのポインターを取得します。 次に、クライアントドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation" data-raw-source="[&lt;strong&gt;USBD_AssignUrbToIoStackLocation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)"><strong>USBD_AssignUrbToIoStackLocation</strong></a>を呼び出して、URB とスタック位置を関連付けます。</td>
</tr>
<tr class="even">
<td>URB を解放するには...</td>
<td>クライアントドライバーによってスタックに URB が割り当てられた場合、要求が完了すると、変数はスコープから除外されます。
<p>クライアントドライバーまたは USB ドライバースタックによって非ページプールに割り当てられた URB 構造を解放するために、クライアントドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>Exfreepool</strong></a>を呼び出します。</p></td>
<td>クライアントドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree" data-raw-source="[&lt;strong&gt;USBD_UrbFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)"><strong>USBD_UrbFree</strong></a>を呼び出します。</td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>関連トピック

[USB デバイスへの要求の送信](communicating-with-a-usb-device.md)  
