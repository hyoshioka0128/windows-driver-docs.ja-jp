---
Description: USB クライアントドライバーが USB ドライバースタックへの URBs の割り当て、ビルド、および送信を行う方法について説明します。
title: USB 要求ブロック (URBs)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4338c21fc196d02b05496be390e770b9adfa4e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831803"
---
# <a name="usb-request-blocks-urbs"></a>USB 要求ブロック (URBs)


ここでは、usb 要求ブロック (URB) について説明します。また、usb クライアントドライバーが Windows Driver Model (WDM) ルーチンを使用して、URBs を USB ドライバースタックに割り当て、ビルド、および送信する方法についての情報を提供します。

ユニバーサルシリアルバス (USB) クライアントドライバーが、デバイスと直接通信することはできません。 代わりに、クライアントドライバーは要求を作成し、処理のために USB ドライバースタックに送信します。 各要求内で、クライアントドライバーは、 *USB 要求ブロック (URB)* と呼ばれる可変長データ構造を提供します。 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体は、要求の詳細を記述します。また、完了した要求の状態に関する情報も含まれます。 クライアントドライバーは、URBs を介して、データ転送を含む、デバイス固有のすべての操作を実行します。 クライアントドライバーは、USB ドライバースタックに送信する前に、要求に関する情報を使用して URB を初期化する必要があります。 Microsoft は、特定の種類の要求について、 **urb**構造体を割り当て、クライアントドライバーによって提供される詳細を使用して、 **urb**構造体に必要なメンバーを埋めるヘルパールーチンとマクロを提供します。

各 URB は、要求された操作の種類を識別する目的を持つ標準の固定サイズのヘッダー ([ **\_URB\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_header)) で開始されます。 **\_urb\_HEADER**の**Length**メンバーは、urb のサイズ (バイト単位) を指定します。 **関数**メンバーは、一連のシステム定義の URB\_関数\_XXX 定数の1つである必要があり、要求される操作の種類を決定します。 たとえば、データ転送の場合、このメンバーは転送の種類を示します。 関数コード URB\_関数\_制御\_転送、URB\_関数\_一括\_または\_割り込み\_転送、および URB\_関数\_ISOCH\_TRANSFER は制御を示します、バルク/割り込み、およびアイソクロナス転送それぞれ。 USB ドライバースタックは、 **status**メンバーを使用して、usb 固有のステータスコードを返します。

URB を送信するために、クライアントドライバーは[**IOCTL\_内部\_USB\_submit\_URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)要求を使用します。この要求は、i/o 要求パケット (irp) 型の[**irp\_MJ\_internal @no__t_ によってデバイスに配信され10_ デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)。

USB ドライバースタックが URB の処理を完了すると、ドライバースタックは[**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造体の**status**メンバーを使用して、usb 固有のステータスコードを返します。

**注**  kmdf と UMDF ドライバーの開発者は、それぞれのフレームワークインターフェイスを使用して、USB デバイスと通信する必要があります。 詳細については、「KMDF ドライバー用の[Usb デバイスの操作](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices)」および「 [UMDF での usb インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers)の使用」を参照してください。 これらのトピックでは、USB デバイスの通信に使用される、基になる WDM ドライバーのインターフェイスについて説明します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="how-to-add-xrb-support-for-client-drivers.md" data-raw-source="[Allocating and Building URBs](how-to-add-xrb-support-for-client-drivers.md)">URBs の割り当てとビルド</a></p></td>
<td><p>このトピックでは、USB クライアントドライバーが Windows Driver Model (WDM) ドライバールーチンを使用して、Microsoft 提供の USB ドライバースタックに要求を送信する前に、URB の割り当てとフォーマットを行う方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="send-requests-to-the-usb-driver-stack.md" data-raw-source="[How to Submit an URB](send-requests-to-the-usb-driver-stack.md)">URB を送信する方法</a></p></td>
<td><p>このトピックでは、初期化された URB を USB ドライバースタックに送信して特定の要求を処理するために必要な手順について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-client-driver-contract-in-windows-8.md" data-raw-source="[Best Practices: Using URBs](usb-client-driver-contract-in-windows-8.md)">ベストプラクティス: URBs の使用</a></p></td>
<td><p>このトピックでは、Windows 8 に含まれる USB ドライバースタックへの URB の割り当て、構築、および送信を行うためのクライアントドライバーのベストプラクティスについて説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



