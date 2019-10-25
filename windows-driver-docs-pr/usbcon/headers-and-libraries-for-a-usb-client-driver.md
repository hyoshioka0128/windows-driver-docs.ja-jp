---
Description: このトピックでは、Windows Driver Model (WDM) USB クライアントドライバーの作成に必要なヘッダーとライブラリを示します。
title: USB クライアント ドライバーで必要なヘッダーとライブラリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ce12d6cdfd4b3f3862f6f352a869694c41b8333
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844997"
---
# <a name="headers-and-libraries-required-by-a-usb-client-driver"></a>USB クライアント ドライバーで必要なヘッダーとライブラリ


このトピックでは、Windows Driver Model (WDM) USB クライアントドライバーの作成に必要なヘッダーとライブラリを示します。

特定のデバイスドライバーインターフェイス (DDI) のヘッダーとライブラリを検索するには、 [USB リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/)の参照ページを参照してください。

## <a name="headers"></a>ヘッダー


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>ヘッダーファイル</th>
<th>Path</th>
<th>が含まれ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>hubbusif</td>
<td>Include/km</td>
<td></td>
<td>Usb ポートドライバーによってエクスポートされ、USB ハブドライバーで使用できるようにするサービスを定義します。</td>
</tr>
<tr class="even">
<td>usb. h</td>
<td>Include\ 共有</td>
<td></td>
<td>USB ドライバースタックに要求を送信するためにクライアントドライバーが必要とする、USB 要求ブロック (URBs) の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>構造を定義します。</td>
</tr>
<tr class="odd">
<td>usb100</td>
<td>Include\ 共有</td>
<td></td>
<td>公式 USB 1.0 仕様に従って、USB 記述子を定義します。</td>
</tr>
<tr class="even">
<td>usb200</td>
<td>Include\ 共有</td>
<td><p>usb100</p></td>
<td>公式 USB 2.0 仕様に従って、USB 記述子を定義します。</td>
</tr>
<tr class="odd">
<td>usbbusif .h</td>
<td>Include/km</td>
<td></td>
<td>Usbd に直接リンクするのではなく、ポートドライバーに直接リンクする必要がある USB クライアントドライバー (FDO) に対して定義されているバスインターフェイスを定義します。</td>
</tr>
<tr class="even">
<td>usbdi. h</td>
<td>Include\ 共有</td>
<td><p>usb. h</p>
<p>usbioctl</p></td>
<td>特定の種類の要求に対して URBs を書式設定するためのヘルパーマクロを定義します。</td>
</tr>
<tr class="odd">
<td>usbdlib. h</td>
<td>Include/km</td>
<td></td>
<td>Usb ドライバースタックに要求を送信するために USB クライアントドライバーによって使用される DDIs を定義します。</td>
</tr>
<tr class="even">
<td>usbdrivr</td>
<td>Include/km</td>
<td><p>usb. h</p>
<p>usbdlib. h</p>
<p>usbioctl</p>
<p>usbbusif .h</p></td>
<td>USB_KERNEL_IOCTL を定義します。</td>
</tr>
<tr class="odd">
<td>usbioctl</td>
<td>Include\ 共有</td>
<td><p>usbiodef</p>
<p>usb200</p></td>
<td>USB ドライバースタックでサポートされる IOCTL コードを定義します。 クライアントドライバーのカーネルモード IOCTL コードを含みます。アプリケーションのユーザーモード IOCTL コード。</td>
</tr>
<tr class="even">
<td>usbiodef</td>
<td>Include\ 共有</td>
<td></td>
<td>インターフェイスと WMI の Guid を定義します。</td>
</tr>
<tr class="odd">
<td>usbkern。 h</td>
<td>Include/km</td>
<td><p>usbioctl</p></td>
<td>使用しないでください。</td>
</tr>
<tr class="even">
<td>usbrpmif. h</td>
<td>Include\ um</td>
<td><p>usb100</p>
<p>windef. h</p>
<p>winapifamily .h</p></td>
<td>アプリケーションが USB デバイスのドライバーリダイレクト操作を実行するために自身を登録するための関数を定義します。</td>
</tr>
<tr class="odd">
<td>usbspec. h</td>
<td>Include\ 共有</td>
<td></td>
<td>公式の USB 仕様に従って、デバイスドライバーのインターフェイスを定義します。</td>
</tr>
<tr class="even">
<td>usbuser. h</td>
<td>Include\ um</td>
<td></td>
<td>USB ポートドライバーでサポートされているユーザーモードの IOCTL コードを定義します。</td>
</tr>
<tr class="odd">
<td>winusb. h</td>
<td>Include\ um</td>
<td><p>winapifamily .h</p>
<p>winusbio. h</p></td>
<td>Winusb .dll によって公開される<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">winusb 関数</a>を定義します。この機能は、usb デバイスの関数ドライバーとしてインストールされている winusb に要求を送信するアプリケーションによって使用されます。</td>
</tr>
<tr class="even">
<td>winusbio. h</td>
<td>Include\ 共有</td>
<td><p>winapifamily .h</p>
<p>usb. h</p></td>
<td><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">Winusb 関数</a>のフラグを定義します。</td>
</tr>
</tbody>
</table>

 

## <a name="libraries"></a>ライブラリ


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Library</th>
<th>Path</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>usbd</td>
<td><p>\ Lib& win8em&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\ Lib& winv6.2&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>USB ドライバースタックから情報を取得し、要求の URBs を書式設定するためのヘルパールーチンを提供します。</td>
</tr>
<tr class="even">
<td>usbrpm .lib</td>
<td><p>\ Lib& win8em&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\ Lib& winv6.2&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>Microsoft 提供のドライバーをサードパーティの RPM ドライバーに置き換える操作をアプリケーションで実行するための機能を提供します。</td>
</tr>
<tr class="odd">
<td>usbdex .lib</td>
<td><p>\ Lib& win8em&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\ Lib& winv6.2&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>クライアントドライバーが基になる USB ドライバースタックに要求を送信するためのヘルパールーチンを提供します。 ライブラリは、構築時にクライアントドライバーモジュールに読み込まれ、静的にリンクされます。 これらのルーチンを呼び出すクライアントドライバーは、Windows Vista 以降のバージョンの Windows で実行できます。</td>
</tr>
<tr class="even">
<td>winusb .lib</td>
<td><p>\ Lib& win8em&lt;em&gt;&lt;arch&gt;</em></p>
<p>\ Lib& win8\ um&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\um&lt;em&gt;&lt;arch&gt;</em></p>
<p>\ Lib& winv6.2&lt;em&gt;&lt;arch&gt;</em></p>
<p>\ Lib& winv6.3 3\ um&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>ユーザーモードのクライアントドライバーまたはアプリケーションが、関数ドライバーとして Winusb .sys を読み込んだ USB デバイスと通信するための機能を提供します。</td>
</tr>
</tbody>
</table>

 

## <a name="header-changes-in-windows8"></a>Windows 8 でのヘッダーの変更点


Windows 8 用 Windows Driver Kit (WDK) 以降では、ヘッダーファイル usbspec. h は USBProtocolDefs を置き換えます。

新しいヘッダーファイルである usbspec は、公式の USB 仕様に従って定義されている DDIs のプロトコル定義を提供します。 ヘッダーファイルには、USB 3.0 仕様の DDIs が含まれています。

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
[Windows Driver Kit (WDK) のヘッダー ファイル](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/header-files-in-the-windows-driver-kit)  
[USB クライアント ドライバー開発の概要](getting-started-with-usb-client-driver-development.md)  



