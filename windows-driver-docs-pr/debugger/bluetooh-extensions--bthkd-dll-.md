---
title: Bluetooth 拡張機能 (Bthkd.dll)
description: Bluetooth デバッガー拡張機能は、ターゲット システムの現在の Bluetooth 環境に関する情報を表示します。
ms.assetid: F6C5295D-F1F9-4180-BE57-A7D47AC8690C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4614b6d713ce2fa49b094f15e2555f41ec076046
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582566"
---
# <a name="bluetooth-extensions-bthkddll"></a>Bluetooth 拡張機能 (Bthkd.dll)


Bluetooth デバッガー拡張機能は、ターゲット システムの現在の Bluetooth 環境に関する情報を表示します。

**注**  Bluetooth の拡張機能のデバッグを使用する際は、ドキュメントに未記載の動作または Api に遭遇したことがあります。 私たちがドキュメントに未記載の動作に依存することを強くお勧めします。 または、Api が、将来のリリース変更します。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-bthdevinfo.md" data-raw-source="[!bthkd.bthdevinfo](-bthkd-bthdevinfo.md)">!bthkd.bthdevinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthdevinfo.md" data-raw-source="[!bthkd.bthdevinfo](-bthkd-bthdevinfo.md)">! Bthkd.bthdevinfo</a></strong>コマンドは、指定された作成 BTHENUM デバイス PDO に関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthenuminfo.md" data-raw-source="[!bthkd.bthenuminfo](-bthkd-bthenuminfo.md)">!bthkd.bthenuminfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthenuminfo.md" data-raw-source="[!bthkd.bthenuminfo](-bthkd-bthenuminfo.md)">! Bthkd.bthenuminfo</a></strong>コマンド BTHENUM FDO に関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-bthinfo-.md" data-raw-source="[!bthkd.bthinfo](-bthkd-bthinfo-.md)">!bthkd.bthinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthinfo-.md" data-raw-source="[!bthkd.bthinfo](-bthkd-bthinfo-.md)">! Bthkd.bthinfo</a></strong>コマンド BTHPORT FDO に関する詳細を表示します。 このコマンドは Bluetooth 調査の開始点の他の Bluetooth デバッグ拡張機能コマンドの多くへのアクセスに使用できるアドレス情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthhelp.md" data-raw-source="[!bthkd.bthhelp](-bthkd-bthhelp.md)">!bthkd.bthhelp</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthhelp.md" data-raw-source="[!bthkd.bthhelp](-bthkd-bthhelp.md)">! Bthkd.bthhelp</a></strong>コマンドは、Bluetooth のデバッグ拡張機能コマンドのヘルプを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-bthtree.md" data-raw-source="[!bthkd.bthtree](-bthkd-bthtree.md)">!bthkd.bthtree</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthtree.md" data-raw-source="[!bthkd.bthtree](-bthkd-bthtree.md)">! Bthkd.bthtree</a></strong>コマンドは、Bluetooth デバイスは完全なツリーを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthusbtransfer.md" data-raw-source="[!bthkd.bthusbtransfer](-bthkd-bthusbtransfer.md)">!bthkd.bthusbtransfer</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthusbtransfer.md" data-raw-source="[!bthkd.bthusbtransfer](-bthkd-bthusbtransfer.md)">! Bthkd.bthusbtransfer</a></strong>コマンド Irp、Bip 転送バッファー情報を含む Bluetooth usb 転送コンテキストを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-dibflags.md" data-raw-source="[!bthkd.dibflags](-bthkd-dibflags.md)">! bthkd.dibflags</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-dibflags.md" data-raw-source="[!bthkd.dibflags](-bthkd-dibflags.md)">! Bthkd.dibflags</a></strong>コマンド DEVICE_INFO_BLOCK を表示します。DibFlags は、_DEVICE_INFO_BLOCK でフラグ セットをダンプします。DibFlags します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-hcicmd.md" data-raw-source="[!bthkd.hcicmd](-bthkd-hcicmd.md)">!bthkd.hcicmd</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-hcicmd.md" data-raw-source="[!bthkd.hcicmd](-bthkd-hcicmd.md)">! Bthkd.hcicmd</a></strong>コマンドは、現在保留中のコマンドの一覧を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-hciinterface.md" data-raw-source="[!bthkd.hciinterface](-bthkd-hciinterface.md)">!bthkd.hciinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-hciinterface.md" data-raw-source="[!bthkd.hciinterface](-bthkd-hciinterface.md)">! Bthkd.hciinterface</a></strong>コマンドの表示、bthport! _HCI_INTERFACE 構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-l2capinterface-.md" data-raw-source="[!bthkd.l2capinterface](-bthkd-l2capinterface-.md)">! bthkd.l2capinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-l2capinterface-.md" data-raw-source="[!bthkd.l2capinterface](-bthkd-l2capinterface-.md)">! Bthkd.l2capinterface</a></strong>コマンド L2CAP インターフェイスに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-rfcomminfo.md" data-raw-source="[!bthkd.rfcomminfo](-bthkd-rfcomminfo.md)">!bthkd.rfcomminfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcomminfo.md" data-raw-source="[!bthkd.rfcomminfo](-bthkd-rfcomminfo.md)">! Bthkd.rfcomminfo</a></strong>コマンド RFCOMM FDO と TDI デバイス オブジェクトに関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-rfcommconnection.md" data-raw-source="[!bthkd.rfcommconnection](-bthkd-rfcommconnection.md)">!bthkd.rfcommconnection</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcommconnection.md" data-raw-source="[!bthkd.rfcommconnection](-bthkd-rfcommconnection.md)">! Bthkd.rfcommconnection</a></strong>コマンドは、指定した RFCOMM 接続オブジェクトに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-rfcommchannel.md" data-raw-source="[!bthkd.rfcommchannel](-bthkd-rfcommchannel.md)">!bthkd.rfcommchannel</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcommchannel.md" data-raw-source="[!bthkd.rfcommchannel](-bthkd-rfcommchannel.md)">! Bthkd.rfcommchannel</a></strong>コマンドは、特定の RFCOMM チャネル CB に関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-sdpinterface.md" data-raw-source="[!bthkd.sdpinterface](-bthkd-sdpinterface.md)">!bthkd.sdpinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpinterface.md" data-raw-source="[!bthkd.sdpinterface](-bthkd-sdpinterface.md)">! Bthkd.sdpinterface</a></strong>コマンドは、SDP インターフェイスに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-scointerface-.md" data-raw-source="[!bthkd.scointerface](-bthkd-scointerface-.md)">!bthkd.scointerface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-scointerface-.md" data-raw-source="[!bthkd.scointerface](-bthkd-scointerface-.md)">! Bthkd.scointerface</a></strong>コマンド SCO インターフェイスに関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-sdpnode.md" data-raw-source="[!bthkd.sdpnode](-bthkd-sdpnode.md)">!bthkd.sdpnode</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpnode.md" data-raw-source="[!bthkd.sdpnode](-bthkd-sdpnode.md)">! Bthkd.sdpnode</a></strong>コマンドが、sdp ツリー内のノードに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-sdpstream.md" data-raw-source="[!bthkd.sdpstream](-bthkd-sdpstream.md)">!bthkd.sdpstream</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpstream.md" data-raw-source="[!bthkd.sdpstream](-bthkd-sdpstream.md)">! Bthkd.sdpstream</a></strong>コマンド SDP ストリームの内容を表示します。</p></td>
</tr>
</tbody>
</table>

 

 

 





