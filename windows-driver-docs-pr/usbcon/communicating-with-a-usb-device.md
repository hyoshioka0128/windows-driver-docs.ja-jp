---
Description: USB クライアント ドライバーと割り当てることができます、ビルド、USB ドライバー スタックへの翻訳の送信を方法に関する情報。
title: USB の要求のブロック (翻訳)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05565efe50edaf7600f4e78de377550d638315f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378360"
---
# <a name="usb-request-blocks-urbs"></a>USB の要求のブロック (翻訳)


このセクションでは、USB 要求ブロック (URB) について説明し、USB クライアント ドライバーが Windows Driver Model (WDM) ルーチンを使用して、割り当て、ビルド、および翻訳を USB ドライバー スタックに送信する方法についての情報を提供します。

ユニバーサル シリアル バス (USB) のクライアント ドライバーは、そのデバイスと直接通信できません。 代わりに、クライアント ドライバーでは、要求を作成し、処理のため USB ドライバー スタックに送信します。 クライアント ドライバーと呼ばれる可変長のデータ構造を提供する、各要求内で、 *USB 要求ブロック (URB)* します。 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)構造は、要求の詳細について説明し、完了した要求の状態に関する情報も含まれます。 クライアント ドライバーでは、data transfers は、翻訳を含む、すべてのデバイスに固有の操作を実行します。 クライアント ドライバーでは、USB ドライバー スタックに送信する前に、要求に関する情報を含む URB を初期化する必要があります。 要求の特定の種類に対して、マイクロソフトでは、ヘルパー ルーチンで、割り当てるマクロが提供しています、 **URB**構造体し、の必要なメンバーを塗りつぶし、 **URB**クライアントによって提供される詳細を含む構造体ドライバー。

各 URB が固定サイズの標準ヘッダーで始まります ([ **\_URB\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_header)) 要求された操作の種類を識別するが目的であります。 **長さ**のメンバー  **\_URB\_ヘッダー** URB のバイト単位のサイズを指定します。 **関数**URB のシステム定義の一連のいずれかを指定する必要があります、メンバー\_関数\_XXX の定数が要求された操作の種類を決定します。 データの転送の場合、このメンバーの種類を示します転送します。 関数コード URB\_関数\_コントロール\_転送, URB\_関数\_一括\_または\_INTERRUPT\_転送、および URB\_関数\_アイソクロナス\_転送コントロールや一括/割り込みアイソクロナス転送をそれぞれ示します。 USB ドライバー スタックを使用して、**状態**USB に固有の状態コードを返すメンバー。

クライアント ドライバーを使用して、URB を送信する、 [ **IOCTL\_内部\_USB\_送信\_URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)要求は、の方法で、デバイスに配信されます型の I/O 要求パケット (IRP) の[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)します。

ドライバー スタックの完了後、USB URB を処理するには、ドライバー スタックを使用して、**状態**のメンバー、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb) USB に固有の状態コードを返す構造体。

**注**  KMDF および UMDF ドライバー開発者は、USB デバイスと通信するため各フレームワーク インターフェイスを使用する必要があります。 詳細については、次を参照してください。 [USB デバイスを使用して](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices)KMDF ドライバーおよび[UMDF で USB インターフェイスの操作](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers)します。 これらのトピックでは、USB デバイスの通信に使用される基になる WDM ドライバー インターフェイスについて説明します。

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
<td><p><a href="how-to-add-xrb-support-for-client-drivers.md" data-raw-source="[Allocating and Building URBs](how-to-add-xrb-support-for-client-drivers.md)">割り当てと翻訳の構築</a></p></td>
<td><p>このトピックでは、Microsoft 提供の USB ドライバー スタックに要求を送信する前に、URB を書式設定を割り当てたり、USB クライアント ドライバーが Windows Driver Model (WDM) ドライバーのルーチンを使用する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="send-requests-to-the-usb-driver-stack.md" data-raw-source="[How to Submit an URB](send-requests-to-the-usb-driver-stack.md)">URB を送信する方法</a></p></td>
<td><p>このトピックでは、USB ドライバー スタックに特定の要求を処理するのに初期化された URB を送信するために必要な手順について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-client-driver-contract-in-windows-8.md" data-raw-source="[Best Practices: Using URBs](usb-client-driver-contract-in-windows-8.md)">ベスト プラクティス:翻訳を使用します。</a></p></td>
<td><p>このトピックでは、割り当て、構築、および Windows 8 に含まれている USB ドライバー スタックへ、URB の送信用のクライアント ドライバーのベスト プラクティスについて説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



