---
Description: Information about how a USB client driver can allocate, build, and submit URBs to the USB driver stack.
title: USB の要求のブロック (翻訳)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10e673cae9dc108dd44d28bcb841f045530eb490
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579104"
---
# <a name="usb-request-blocks-urbs"></a>USB の要求のブロック (翻訳)


このセクションでは、USB 要求ブロック (URB) について説明し、USB クライアント ドライバーが Windows Driver Model (WDM) ルーチンを使用して、割り当て、ビルド、および翻訳を USB ドライバー スタックに送信する方法についての情報を提供します。

ユニバーサル シリアル バス (USB) のクライアント ドライバーは、そのデバイスと直接通信できません。 代わりに、クライアント ドライバーでは、要求を作成し、処理のため USB ドライバー スタックに送信します。 クライアント ドライバーと呼ばれる可変長のデータ構造を提供する、各要求内で、 *USB 要求ブロック (URB)* します。 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造は、要求の詳細について説明し、完了した要求の状態に関する情報も含まれます。 クライアント ドライバーでは、data transfers は、翻訳を含む、すべてのデバイスに固有の操作を実行します。 クライアント ドライバーでは、USB ドライバー スタックに送信する前に、要求に関する情報を含む URB を初期化する必要があります。 要求の特定の種類に対して、マイクロソフトでは、ヘルパー ルーチンで、割り当てるマクロが提供しています、 **URB**構造体し、の必要なメンバーを塗りつぶし、 **URB**クライアントによって提供される詳細を含む構造体ドライバー。

各 URB が固定サイズの標準ヘッダーで始まります ([**\_URB\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff540409)) 要求された操作の種類を識別するが目的であります。 **長さ**のメンバー  **\_URB\_ヘッダー** URB のバイト単位のサイズを指定します。 **関数**URB のシステム定義の一連のいずれかを指定する必要があります、メンバー\_関数\_XXX の定数が要求された操作の種類を決定します。 データの転送の場合、このメンバーの種類を示します転送します。 関数コード URB\_関数\_コントロール\_転送, URB\_関数\_一括\_または\_INTERRUPT\_転送、および URB\_関数\_アイソクロナス\_転送コントロールや一括/割り込みアイソクロナス転送をそれぞれ示します。 USB ドライバー スタックを使用して、**状態**USB に固有の状態コードを返すメンバー。

クライアント ドライバーを使用して、URB を送信する、 [ **IOCTL\_内部\_USB\_送信\_URB** ](https://msdn.microsoft.com/library/windows/hardware/ff537271)要求は、の方法で、デバイスに配信されます型の I/O 要求パケット (IRP) の[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)します。

ドライバー スタックの完了後、USB URB を処理するには、ドライバー スタックを使用して、**状態**のメンバー、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923) USB に固有の状態コードを返す構造体。

**注**  KMDF および UMDF ドライバー開発者は、USB デバイスと通信するため各フレームワーク インターフェイスを使用する必要があります。 詳細については、[USB デバイスを使用して](https://msdn.microsoft.com/library/windows/hardware/ff553101)KMDF ドライバーおよび[UMDF で USB インターフェイスの操作](https://msdn.microsoft.com/library/windows/hardware/ff561478)を参照してください。 これらのトピックでは、USB デバイスの通信に使用される基になる WDM ドライバー インターフェイスについて説明します。

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



