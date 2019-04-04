---
title: Bluetooth ドライバー スタックの使用
description: Bluetooth ドライバー スタックの使用
ms.assetid: c8a68c30-4cd6-4ee2-a653-7e0c1a28f4cf
keywords:
- Bluetooth の WDK、ドライバー スタック
- ドライバーは、WDK Bluetooth をスタックします。
- WDK Bluetooth スタック
- プラグ アンド プレイの WDK Bluetooth
- PnP WDK Bluetooth
- Irp WDK Bluetooth
- プロファイル ドライバー WDK Bluetooth
- IOCTL_INTERNAL_BTH_SUBMIT_BRB
- Bluetooth の WDK、Bluetooth のブロックを要求します。
- BRBs WDK
- Bluetooth 要求ブロック WDK
- IRP_MJ_DEVICE_CONTROL
- IRP_MJ_INTERNAL_DEVICE_CONTROL
- Bluetooth の WDK、Ioctl
- Ioctl WDK Bluetooth
- WDK の Bluetooth のリモート接続
- 接続 WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a6441c861987621cee2c56dc0d7188db4cc2902
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571254"
---
# <a name="using-the-bluetooth-driver-stack"></a>Bluetooth ドライバー スタックの使用


Windows のロードし、Bluetooth ドライバー スタックの初期化、後に、ドライバー スタックは既にペアになっているアクティブな Bluetooth デバイスを検出します。 ドライバー スタックは、すべてのペアになっているデバイスのデバイスの id (デバイス Id) を生成します。 次に、ドライバー スタックは標準のプラグ アンド プレイ (PnP) メカニズムを使用して各デバイスのプロファイルを適切なドライバーを読み込みます。 読み込まれるプロファイル ドライバーが選択し、Bluetooth ドライバー スタックが生成するようにプロファイル ドライバーとデバイスの識別子をインストールしで説明されている INF ファイルに基づく[、Bluetooth デバイスのインストール](installing-a-bluetooth-device.md)します。

プロファイル ドライバー WDM アーキテクチャに基づくすべてのドライバーで採用されている標準の I/O 要求パケットの IRP に基づくメカニズムは Bluetooth ドライバー スタックと通信します。 プロファイルのドライバーはの割り当てと Bluetooth ポート ドライバーに Bluetooth ドライバー スタック ダウン Irp を送信して、デバイスと通信*Bthport.sys*します。

プロファイル ドライバーは、初期化によって処理される Irp *Bthport.sys*します。 ドライバーをプロファイルし、自分のデバイスと通信してデバイスに配信される IOCTL 要求を使用して、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)または[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744) IRP します。 プロファイル ドライバーは IRP では、次の一覧で、I/O 制御コードのいずれかを指定します。

Bluetooth ドライバー スタックを介して呼び出し元をカーネル モードの次の Ioctl をサポートしている[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744):

[**IOCTL\_両方\_切断\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff536682)

[**IOCTL\_BTH\_GET\_DEVICE\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536683)

[**IOCTL\_BTH\_GET\_LOCAL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536684)

[**IOCTL\_BTH\_GET\_RADIO\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536685)

[**IOCTL\_BTH\_SDP\_ATTRIBUTE\_SEARCH**](https://msdn.microsoft.com/library/windows/hardware/ff536687)

[**IOCTL\_BTH\_SDP\_CONNECT**](https://msdn.microsoft.com/library/windows/hardware/ff536688)

[**IOCTL\_BTH\_SDP\_DISCONNECT**](https://msdn.microsoft.com/library/windows/hardware/ff536689)

[**IOCTL\_BTH\_SDP\_REMOVE\_RECORD**](https://msdn.microsoft.com/library/windows/hardware/ff536690)

[**IOCTL\_BTH\_SDP\_SERVICE\_ATTRIBUTE\_SEARCH**](https://msdn.microsoft.com/library/windows/hardware/ff536691)

[**IOCTL\_両方\_SDP\_サービス\_検索**](https://msdn.microsoft.com/library/windows/hardware/ff536692)

[**IOCTL\_BTH\_SDP\_SUBMIT\_RECORD**](https://msdn.microsoft.com/library/windows/hardware/ff536693)

[**IOCTL\_BTH\_SDP\_SUBMIT\_RECORD\_WITH\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536694)

Bluetooth ドライバー スタックは、次の Ioctl をサポートしていると[ **BRBs** ](https://msdn.microsoft.com/library/windows/hardware/ff536607)を介して (通常、ドライバーの通信用)、カーネル モードの呼び出し元[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766):

[**BRB\_HCI\_GET\_LOCAL\_BD\_ADDR**](https://msdn.microsoft.com/library/windows/hardware/ff536611)

[**BRB\_L2CA\_登録\_サーバー**](https://msdn.microsoft.com/library/windows/hardware/ff536618)

[**BRB\_L2CA\_登録解除\_サーバー**](https://msdn.microsoft.com/library/windows/hardware/ff536619)

[**BRB\_L2CA\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536615)

[**BRB\_L2CA\_オープン\_チャネル\_応答**](https://msdn.microsoft.com/library/windows/hardware/ff536616)

[**BRB\_L2CA\_閉じる\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536614)

[**BRB\_L2CA\_ACL\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff536613)

[**BRB\_L2CA\_UPDATE\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536620)

[**BRB\_L2CA\_PING**](https://msdn.microsoft.com/library/windows/hardware/ff536617)

[**BRB\_登録\_PSM**](https://msdn.microsoft.com/library/windows/hardware/ff536621)

[**BRB\_登録解除\_PSM**](https://msdn.microsoft.com/library/windows/hardware/ff536632)

[**BRB\_SCO\_登録\_サーバー**](https://msdn.microsoft.com/library/windows/hardware/ff536628)

[**BRB\_SCO\_登録解除\_サーバー**](https://msdn.microsoft.com/library/windows/hardware/ff536630)

[**BRB\_SCO\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536626)

[**BRB\_SCO\_オープン\_チャネル\_応答**](https://msdn.microsoft.com/library/windows/hardware/ff536627)

[**BRB\_SCO\_閉じる\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536622)

[**BRB\_SCO\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff536629)

[**BRB\_SCO\_取得\_チャネル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536624)

[**BRB\_SCO\_取得\_システム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536625)

[**BRB\_SCO\_フラッシュ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536623)

[**BRB\_ACL\_取得\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff536609)

[**BRB\_ACL\_ENTER\_ACTIVE\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff536608)

[**BRB\_取得\_デバイス\_インターフェイス\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff536610)

[**IOCTL\_内部\_両方\_送信\_BRB**](https://msdn.microsoft.com/library/windows/hardware/ff536751)

[**IOCTL\_内部\_BTHENUM\_取得\_DEVINFO**](https://msdn.microsoft.com/library/windows/hardware/ff536748)

[**IOCTL\_内部\_BTHENUM\_取得\_ENUMINFO**](https://msdn.microsoft.com/library/windows/hardware/ff536750)

前の一覧で説明されている Ioctl を使用する方法の詳細については、[Bluetooth Ioctl](bluetooth-ioctls2.md)を参照してください。

プロファイルのドライバーでは、IOCTL 主に使用して\_内部\_両方\_送信\_BRB と通信して、Bluetooth ドライバー スタックで提供される機能と対話します。 プロファイルのドライバーは IOCTL\_内部\_両方\_送信\_BRB 可変長のデータ構造を提供するには Bluetooth 要求のブロックが呼び出されます ( [ **BRB** ](https://msdn.microsoft.com/library/windows/hardware/ff536607))デバイスを管理します。 プロファイルのドライバーは、リモート デバイスへの接続を開いたり閉じたりして、入力と出力のほとんどのタスクを実行する BRBs を使用します。 IOCTL\_内部\_両方\_送信\_BRB には、Bluetooth の操作を実行する詳細を説明する BRB が含まれています。 構築し、Bluetooth ドライバー スタック ダウン BRBs を送信する方法の詳細については、[のビルドと送信を BRB](building-and-sending-a-brb.md)を参照してください。

各 BRB がによって定義されている標準ヘッダーで始まる、 [ **BRB\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff536612)構造、BRB の残りの部分の構造を決定する、BRB の型を指定します。 **型**で見つかった値のいずれかでなければなりませんメンバー、 [ **BRB\_型**](https://msdn.microsoft.com/library/windows/hardware/ff536631)列挙型では、Bluetooth 操作の種類を決定しますが、。ドライバーの要求をプロファイルします。 サイズと BRB 構造は、BRB の種類に応じて変わります。 **長さ**、BRB のメンバー\_ヘッダー構造、BRB のバイト単位のサイズを指定します。 [ **BthAllocateBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536634)、 [ **BthInitializeBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536639)、および[ **BthReuseBrb**](https://msdn.microsoft.com/library/windows/hardware/ff536640)関数が自動的に設定、**型**と**長さ**メンバー。

たとえば、リモート デバイスへの接続を開くには、関数コードでは、いずれかを指定**BRB\_L2CA\_開く\_チャネル**または BRB\_SCO\_オープン\_をプロファイル ドライバーが、L2CAP またはリモート デバイスに SCO 接続チャネルを開こうとしたことを示すために、チャネル。 Bluetooth ドライバー スタックを使用して、**状態**Bluetooth に固有の状態コードを返す BRB 構造体のメンバー。

各 BRB、プロファイルのドライバーでは割り当てを実行する Bluetooth 操作に関する情報を適切な対応する構造体を初期化する必要があります。

次の表では、プロファイルのドライバーを発行する特定の BRBs に対応する構造体について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bluetooth の要求のブロック (BRB)</th>
<th align="left">対応する構造体</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BRB_HCI_GET_LOCAL_BD_ADDR</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536857" data-raw-source="[&lt;strong&gt;_BRB_GET_LOCAL_BD_ADDR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536857)"><strong>_BRB_GET_LOCAL_BD_ADDR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536862" data-raw-source="[&lt;strong&gt;_BRB_L2CA_REGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536862)"><strong>_BRB_L2CA_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536863" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UNREGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536863)"><strong>_BRB_L2CA_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536860" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536860)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536860" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536860)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536859" data-raw-source="[&lt;strong&gt;_BRB_L2CA_CLOSE_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536859)"><strong>_BRB_L2CA_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_ACL_TRANSFER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536858" data-raw-source="[&lt;strong&gt;_BRB_L2CA_ACL_TRANSFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536858)"><strong>_BRB_L2CA_ACL_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_UPDATE_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536864" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UPDATE_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536864)"><strong>_BRB_L2CA_UPDATE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_PING</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536861" data-raw-source="[&lt;strong&gt;_BRB_L2CA_PING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536861)"><strong>_BRB_L2CA_PING</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_REGISTER_PSM</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536865" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536865)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_UNREGISTER_PSM</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536865" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536865)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536871" data-raw-source="[&lt;strong&gt;_BRB_SCO_REGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536871)"><strong>_BRB_SCO_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536873" data-raw-source="[&lt;strong&gt;_BRB_SCO_UNREGISTER_SERVER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536873)"><strong>_BRB_SCO_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536870" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536870)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536870" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536870)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536866" data-raw-source="[&lt;strong&gt;_BRB_SCO_CLOSE_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536866)"><strong>_BRB_SCO_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_TRANSFER</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536872" data-raw-source="[&lt;strong&gt;_BRB_SCO_TRANSFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536872)"><strong>_BRB_SCO_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_GET_CHANNEL_INFO</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536868" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_CHANNEL_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536868)"><strong>_BRB_SCO_GET_CHANNEL_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_GET_SYSTEM_INFO</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536869" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_SYSTEM_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536869)"><strong>_BRB_SCO_GET_SYSTEM_INFO</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_FLUSH_CHANNEL</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536867" data-raw-source="[&lt;strong&gt;_BRB_SCO_FLUSH_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536867)"><strong>_BRB_SCO_FLUSH_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_ACL_GET_MODE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536855" data-raw-source="[&lt;strong&gt;_BRB_ACL_GET_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536855)"><strong>_BRB_ACL_GET_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_ACL_ENTER_ACTIVE_MODE</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536854" data-raw-source="[&lt;strong&gt;_BRB_ACL_ENTER_ACTIVE_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536854)"><strong>_BRB_ACL_ENTER_ACTIVE_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_GET_DEVICE_INTERFACE_STRING</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536856" data-raw-source="[&lt;strong&gt;_BRB_GET_DEVICE_INTERFACE_STRING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536856)"><strong>_BRB_GET_DEVICE_INTERFACE_STRING</strong></a></p></td>
</tr>
</tbody>
</table>

 

Bluetooth の Ioctl および BRBs の使用に関する詳細については、[のビルドと送信を BRB](building-and-sending-a-brb.md)を参照してください。

 

 





