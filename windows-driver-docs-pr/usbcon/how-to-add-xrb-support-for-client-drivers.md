---
Description: このトピックでは、Microsoft 提供の USB ドライバー スタックに要求を送信する前に、URB を書式設定を割り当てたり、USB クライアント ドライバーが Windows Driver Model (WDM) ドライバーのルーチンを使用する方法について説明します。
title: URB の割り当てと構築
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d09e3df17b36199ecae09fd6ffcaaaf7a19d763e
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405048"
---
# <a name="allocating-and-building-urbs"></a>URB の割り当てと構築

USB クライアント ドライバーでは、Microsoft 提供の USB ドライバー スタックに要求を送信する前に、URB を書式設定を割り当てたり、Windows Driver Model (WDM) ドライバーのルーチンを使用できます。

クライアント ドライバーでは、USB ドライバー スタックの下位のドライバーで要求を処理するのにために必要なすべての情報をパッケージ化するのに、URB を使用します。 Windows オペレーティング システムで、URB が説明されている、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体。

Microsoft 提供のライブラリ[USB クライアント ドライバーのルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#client)します。 これらのルーチンを使用すると、USB クライアント ドライバーは URB 要求の特定の指定された操作をビルドし、下位の USB スタックに転送できます。 場合は、ライブラリ ルーチンを呼び出す独自 URB 要求を作成するのではなく、サポートされている操作は、クライアント ドライバーを設計できます。

## <a name="urb-allocation-in-windows7-and-earlier"></a>Windows 7 およびそれ以前で URB 割り当て

を Windows 7 および Windows の以前のバージョンの Windows Driver Kit (WDK) で含まれているルーチンを使用して USB 要求を送信するクライアント ドライバー通常割り当てし、設定、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造、関連付け、**URB**新しい IRP では、作成して送信し、USB ドライバー スタックに IRP の構造体。

要求の特定の種類では、Microsoft が提供します (しくみによってエクスポート) を割り当てるヘルパー ルーチンと形式、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体。 たとえば、 [ **USBD\_CreateConfigurationRequestEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539029)ルーチン用のメモリを割り当て、 **URB**構造体の URB を書式設定、構成の要求のアドレスを返します、 **URB**クライアント ドライバーに構造体。 ただし、ヘルパー ルーチンは、すべての種類の要求は使用できません。

Microsoft では、要求の種類によっては翻訳を書式設定されたマクロも提供します。 これらのマクロでは、クライアント ドライバーを割り当てる必要があります、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)呼び出して構造[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)を割り当てるか、スタックに構造体。 たとえば、クライアント ドライバーが割り当てた後、 **URB**、ドライバーを呼び出すことができます[ **UsbBuildSelectConfigurationRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538968)選択構成 URB を書式設定するには要求または構成をクリアします。

クライアント ドライバーの割り当てし、URB を手動でのさまざまなメンバーを設定して書式設定する必要がありますの要求を他の[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体には、要求の種類によって異なります。

USB の要求が完了したら、クライアント ドライバーをリリースする必要があります、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体。 URB がスタックに割り当てられている場合、URB はスコープ外になったときに解放されます。 URB が非ページ プールに割り当てられている場合、クライアント ドライバーを呼び出す必要があります[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590) URB を解放します。

## <a name="urb-allocation-in-windows8"></a>Windows 8 で URB 割り当て

Windows 8 WDK 用では、新規のスタティック ライブラリ、割り当て、書式設定、および翻訳を解放するためのルーチンをエクスポートする Usbdex.lib を提供します。 さらに、IRP を URB に関連付ける新しい方法があります。 Windows Vista および Windows の以降のバージョンを対象とするクライアント ドライバーによって新しいルーチンを呼び出すことができます。

Windows Vista 以降を実行しているクライアント ドライバーは、新しいルーチンを使用して、基になる USB ドライバー スタックは、特定のパフォーマンスと信頼性機能の強化を利用できるようにする必要があります。 これらの機能強化は、USB 3.0 デバイスおよびホスト コント ローラーをサポートするために Windows 8 で導入された新しい USB ドライバー スタックに適用されます。 USB 2.0 ホスト コント ローラーは、Windows は、機能強化がサポートされていないドライバー スタックの以前のバージョンを読み込みます。 基になるドライバー スタックのバージョンまたはホスト コント ローラーでサポートされているプロトコルのバージョンに関係なく、新しい URB ルーチンを常に呼び出す必要があります。

新しいルーチンのいずれかを呼び出す前に、クライアント ドライバーの登録は USB ドライバー スタックと USBD ハンドルがあることを確認します。 USBD ハンドルを取得するには、呼び出す[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)します。

次のルーチン for Windows 8 WDK で利用できます。 これらのルーチンは、Usbdlib.h で定義されます。

* [**USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)
* [**USBD\_IsochUrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406231)
* [**USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)
* [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)
* [**USBD\_UrbFree**](https://msdn.microsoft.com/library/windows/hardware/hh406252)
* [**USBD\_AssignUrbToIoStackLocation**](https://msdn.microsoft.com/library/windows/hardware/hh406228)

上記の割り当てルーチンが新しいへのポインターを返す[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体は、USB ドライバー スタックによって割り当てられています。 、Windows によって読み込まれた USB ドライバー スタックのバージョンに応じて、 **URB**構造体とする非透過的なペアリング*URB コンテキスト*します。 URB コンテキストは、URB に関する情報のブロックです。 URB ヘッダーの内容を表示することはできません情報は、USB ドライバー スタックが URB を追跡および処理を向上させるために内部的に使用する対象としています。 URB コンテキストが*のみ*for Windows 8 USB ドライバー スタックで使用します。
URB コンテキストを使用できる場合、USB ドライバー スタックはこれを使用して安全性と効率 URB 処理を加えます。 たとえば、USB ドライバー スタックはクライアント ドライバーの URB を送信し、最初の要求が完了する前に、その同じ URB を再利用しようがいないことを確認してください。 その種のエラーを検出するためには、USB ドライバー スタックは、URB コンテキストでの状態情報を格納します。 状態情報がない場合は、USB ドライバー スタックは、現在進行中のすべての翻訳で着信 URB を比較する必要があります。 状態情報は、クライアント ドライバーが URB を解放しようとしたときにも、USB ドライバー スタックで使用されます。 URB をリリースする前に、USB ドライバー スタックは URB が保留中ではないことを確認する状態を確認します。

URB コンテキストでは、余分な URB 情報を格納するための公式のメカニズムを提供します。 URB を使用してコンテキストがの予約済みのメンバーに必要なまたはファイルを格納する追加情報として余分なメモリを割り当てることをお勧め、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体。 USB ドライバー スタックは、翻訳をできるように、今後拡大 URB コンテキストが必要な場合のみ必要な調整プールの割り当てのサイズには非ページ プールは、関連付けられている URB コンテキストを割り当てます。

## <a name="urb-routine-migration"></a>URB 日常的な移行

次の表では、URB ルーチンの変更をまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ユース ケース</th>
<th>WDK の Windows 7 以前のバージョンで利用可能</th>
<th>Windows 8 向けの WDK で使用できます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td>Windows 7 およびそれ以前のバージョンのオペレーティング システムを対象と</td>
<td>Windows Vista およびそれ以降のバージョンのオペレーティング システムを対象と</td>
</tr>
<tr class="even">
<td>URB を作成する.</td>
<td>クライアント ドライバーを割り当てます、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>構造体であり、要求に応じて構造体を書式設定します。
<p>クライアント ドライバーは、スタックに URB 構造体を割り当てまたはドライバーが呼び出すことによって非ページ プール内の構造を割り当てます<a href="https://msdn.microsoft.com/library/windows/hardware/ff544520" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544520)"> <strong>exallocatepoolwithtag に</strong></a>します。</p></td>
<td>クライアント ドライバーの呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/hh406250" data-raw-source="[&lt;strong&gt;USBD_UrbAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406250)"> <strong>USBD_UrbAllocate</strong> </a>新しいへのポインターを受け取ると<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>構造体は、USB によって割り当てられていますドライバー スタックです。 基になる USB ドライバー スタックの USBD インターフェイスのバージョンに応じて、URB コンテキストに関連付けられて URB 場合があります。</td>
</tr>
<tr class="odd">
<td>URB 選択構成要求を作成する.</td>
<td>クライアント ドライバーの呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff539029" data-raw-source="[&lt;strong&gt;USBD_CreateConfigurationRequestEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539029)"> <strong>USBD_CreateConfigurationRequestEx</strong> </a>ルーチンを作成および USB ドライバー スタックで書式設定される新しい URB にポインターを返します。</td>
<td>クライアント ドライバーの呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/hh406243" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406243)"> <strong>USBD_SelectConfigUrbAllocateAndBuild</strong> </a>新しいへのポインターを受け取ると<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>は構造体割り当てられているし、USB ドライバー スタックで (選択構成要求) の書式設定します。 基になる USB ドライバー スタックの USBD インターフェイスのバージョンに応じて、URB コンテキストに関連付けられて URB 場合があります。</td>
</tr>
<tr class="even">
<td>選択インターフェイス要求の URB を作成する.</td>
<td>クライアント ドライバーを割り当てます、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>構造と使用、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540425" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540425)"> <strong>_URB_SELECT_INTERFACE</strong> </a> select の形式を定義する構造体USB デバイスのインターフェイス コマンド。</td>
<td>クライアント ドライバーの呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/hh406245" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406245)"> <strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong> </a>新しいへのポインターを受け取ると<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>される構造割り当てられ、USB ドライバー スタックで (選択インターフェイス要求) の書式設定します。 基になる USB ドライバー スタックの USBD インターフェイスのバージョンに応じて、URB コンテキストに関連付けられて URB 場合があります。</td>
</tr>
<tr class="odd">
<td>IRP を URB を関連付ける.</td>
<td>クライアント ドライバーは IRP スタックの次の位置にポインターを取得します呼び出して<a href="https://msdn.microsoft.com/library/windows/hardware/ff549266" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549266)"> <strong>IoGetNextIrpStackLocation</strong></a>します。 クライアント ドライバーを手動で設定し、 <strong>Parameters.Others.Argument1</strong>スタックの場所のアドレスへのメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>構造体。</td>
<td>クライアント ドライバーは IRP スタックの次の位置にポインターを取得します呼び出して<a href="https://msdn.microsoft.com/library/windows/hardware/ff549266" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549266)"> <strong>IoGetNextIrpStackLocation</strong></a>します。 クライアント ドライバーの呼び出し操作を実行し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh406228" data-raw-source="[&lt;strong&gt;USBD_AssignUrbToIoStackLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406228)"> <strong>USBD_AssignUrbToIoStackLocation</strong> </a>に関連付ける、スタックの場所で URB します。</td>
</tr>
<tr class="even">
<td>URB をリリースする.</td>
<td>クライアント ドライバーがスタック上の URB を割り当てた場合は、要求が完了した後、変数がスコープ外です。
<p>クライアント ドライバーまたは USB ドライバー スタックのクライアント ドライバーを非ページ プールに割り当てられた URB 構造体を解放する呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/ff544590" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544590)"> <strong>ExFreePool</strong></a>します。</p></td>
<td>クライアント ドライバーの呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/hh406252" data-raw-source="[&lt;strong&gt;USBD_UrbFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406252)"> <strong>USBD_UrbFree</strong></a>します。</td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>関連トピック

[USB デバイスに要求を送信](communicating-with-a-usb-device.md)  
