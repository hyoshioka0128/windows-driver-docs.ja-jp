---
Description: このトピックでは、ヘッダーと、Windows Driver Model (WDM) USB クライアント ドライバーを記述するために必要なライブラリを一覧表示します。
title: USB クライアント ドライバーで必要なヘッダーとライブラリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91613d6c66488820ca24f089ffc9cdf68d108571
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347992"
---
# <a name="headers-and-libraries-required-by-a-usb-client-driver"></a>USB クライアント ドライバーで必要なヘッダーとライブラリ


このトピックでは、ヘッダーと、Windows Driver Model (WDM) USB クライアント ドライバーを記述するために必要なライブラリを一覧表示します。

特定のデバイス ドライバー インターフェイス (DDI) のヘッダーとライブラリを検索のリファレンス ページを参照してください。、 [USB 参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/)します。

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
<th>ヘッダー ファイル</th>
<th>パス</th>
<th>含まれています</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>hubbusif.h</td>
<td>Include\km</td>
<td></td>
<td>USB ポート ドライバーによってエクスポートされた、USB ハブのドライバーで使用可能なサービスを定義します。</td>
</tr>
<tr class="even">
<td>usb.h</td>
<td>Include\shared</td>
<td></td>
<td>定義<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a> USB ドライバー スタックに要求を送信するために必要なクライアント ドライバーで USB 要求のブロック (翻訳) の構造体。</td>
</tr>
<tr class="odd">
<td>usb100.h</td>
<td>Include\shared</td>
<td></td>
<td>公式の USB 1.0 仕様に従って、USB 記述子を定義します。</td>
</tr>
<tr class="even">
<td>usb200.h</td>
<td>Include\shared</td>
<td><p>usb100.h</p></td>
<td>公式の USB 2.0 仕様どおりの USB ディスクリプターを定義します。</td>
</tr>
<tr class="odd">
<td>usbbusif.h</td>
<td>Include\km</td>
<td></td>
<td>しくみに直接リンクではなくポート ドライバーに直接リンクする必要があるの USB クライアント ドライバー (FDO) に対して定義されているバス インターフェイスを定義します。</td>
</tr>
<tr class="even">
<td>usbdi.h</td>
<td>Include\shared</td>
<td><p>usb.h</p>
<p>usbioctl.h</p></td>
<td>特定の種類の要求の翻訳を書式設定するためのヘルパー マクロを定義します。</td>
</tr>
<tr class="odd">
<td>usbdlib.h</td>
<td>Include\km</td>
<td></td>
<td>USB ドライバー スタックに要求を送信する USB クライアント ドライバーによって使用される Ddi を定義します。</td>
</tr>
<tr class="even">
<td>usbdrivr.h</td>
<td>Include\km</td>
<td><p>usb.h</p>
<p>usbdlib.h</p>
<p>usbioctl.h</p>
<p>usbbusif.h</p></td>
<td>USB_KERNEL_IOCTL を定義します。</td>
</tr>
<tr class="odd">
<td>usbioctl.h</td>
<td>Include\shared</td>
<td><p>usbiodef.h</p>
<p>usb200.h</p></td>
<td>IOCTL を定義します。 USB ドライバー スタックでサポートされているコード。 クライアント ドライバーのカーネル モードの IOCTL コードが含まれていますアプリケーションのユーザー モードの IOCTL コード。</td>
</tr>
<tr class="even">
<td>usbiodef.h</td>
<td>Include\shared</td>
<td></td>
<td>インターフェイスと WMI の Guid を定義します。</td>
</tr>
<tr class="odd">
<td>usbkern.h</td>
<td>Include\km</td>
<td><p>usbioctl.h</p></td>
<td>使用しないでください。</td>
</tr>
<tr class="even">
<td>usbrpmif.h</td>
<td>Include\um</td>
<td><p>usb100.h</p>
<p>windef.h</p>
<p>winapifamily.h</p></td>
<td>USB デバイスのドライバーのリダイレクトを行うために自身を登録するアプリケーションの関数を定義します。</td>
</tr>
<tr class="odd">
<td>usbspec.h</td>
<td>Include\shared</td>
<td></td>
<td>公式の USB 仕様に従って、デバイス ドライバー インターフェイスを定義します。</td>
</tr>
<tr class="even">
<td>usbuser.h</td>
<td>Include\um</td>
<td></td>
<td>USB ポート ドライバーでサポートされている IOCTL コードをユーザー モードを定義します。</td>
</tr>
<tr class="odd">
<td>winusb.h</td>
<td>Include\um</td>
<td><p>winapifamily.h</p>
<p>winusbio.h</p></td>
<td>定義<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB functions</a> Winusb.dll、によって公開される関数のドライバーを USB デバイスとしてインストールされている Winusb.sys に要求を送信する必要があるアプリケーションによって使用されます。</td>
</tr>
<tr class="even">
<td>winusbio.h</td>
<td>Include\shared</td>
<td><p>winapifamily.h</p>
<p>usb.h</p></td>
<td>フラグを定義<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB functions</a>します。</td>
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
<th>パス</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>usbd.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>USB ドライバー スタックから情報を取得すると、要求の翻訳を書式設定には、ヘルパー ルーチンを提供します。</td>
</tr>
<tr class="even">
<td>usbrpm.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>サード パーティ製の RPM ドライバーを使用した Microsoft から提供されたドライバーを置換するための操作を実行するアプリケーションの機能を提供します。</td>
</tr>
<tr class="odd">
<td>usbdex.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>基になる USB ドライバー スタックに要求を送信するクライアント ドライバー用のヘルパー ルーチンを提供します。 ライブラリは、読み込まれ、ビルド時に、クライアント ドライバーのモジュールに静的にリンクを取得します。 これらのルーチンを呼び出すクライアント ドライバーは、Windows Vista および Windows の以降のバージョンで実行できます。</td>
</tr>
<tr class="even">
<td>winusb.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win8\um&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\um&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\um&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>ユーザー モードのクライアント ドライバーまたは Winusb.sys 関数ドライバーとして読み込まれている USB デバイスと通信するアプリケーションの機能を提供します。</td>
</tr>
</tbody>
</table>

 

## <a name="header-changes-in-windows8"></a>Windows 8 のヘッダーの変更点


Windows Driver Kit (WDK) では、Windows 8 以降、ヘッダー ファイル usbspec.h USBProtocolDefs.h を置き換えます。

新しいヘッダー ファイル、usbspec.h、公式の USB 仕様に従って定義されている Ddi のプロトコルの定義を提供します。 ヘッダー ファイルには、Ddi には for USB 3.0 仕様が含まれています。

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Windows Driver Kit (WDK) のヘッダー ファイル](https://msdn.microsoft.com/library/windows/hardware/ff554695)  
[USB クライアント ドライバー開発の概要](getting-started-with-usb-client-driver-development.md)  



