---
title: Bluetooth ドライバー スタックを使用する方法
description: Bluetooth ドライバー スタックを使用する方法
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
ms.date: 07/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014f124e75494acaf58f53a87ee7f20608545632
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608453"
---
# <a name="how-to-use-the-bluetooth-driver-stack"></a>Bluetooth ドライバー スタックを使用する方法


Windows のロードし、Bluetooth ドライバー スタックの初期化、後に、ドライバー スタックは既にペアになっているアクティブな Bluetooth デバイスを検出します。 ドライバー スタックは、すべてのペアになっているデバイスのデバイスの id (デバイス Id) を生成します。 次に、ドライバー スタックは標準のプラグ アンド プレイ (PnP) メカニズムを使用して各デバイスのプロファイルを適切なドライバーを読み込みます。 読み込まれるプロファイル ドライバーが選択し、Bluetooth ドライバー スタックが生成するようにプロファイル ドライバーとデバイスの識別子をインストールしで説明されている INF ファイルに基づく[、Bluetooth デバイスのインストール](installing-a-bluetooth-device.md)します。

プロファイル ドライバー WDM アーキテクチャに基づくすべてのドライバーで採用されている標準の I/O 要求パケットの IRP に基づくメカニズムは Bluetooth ドライバー スタックと通信します。 プロファイルのドライバーはの割り当てと Bluetooth ポート ドライバーに Bluetooth ドライバー スタック ダウン Irp を送信して、デバイスと通信*Bthport.sys*します。

プロファイル ドライバーは、初期化によって処理される Irp *Bthport.sys*します。 ドライバーをプロファイルし、自分のデバイスと通信してデバイスに配信される IOCTL 要求を使用して、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)または[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) IRP します。 プロファイル ドライバーは IRP では、次の一覧で、I/O 制御コードのいずれかを指定します。

Bluetooth ドライバー スタックを介して呼び出し元をカーネル モードの次の Ioctl をサポートしている[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control):

[**IOCTL\_両方\_切断\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_disconnect_device)

[**IOCTL\_BTH\_GET\_DEVICE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)

[**IOCTL\_BTH\_GET\_LOCAL\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)

[**IOCTL\_BTH\_GET\_RADIO\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)

[**IOCTL\_BTH\_SDP\_ATTRIBUTE\_SEARCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)

[**IOCTL\_BTH\_SDP\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)

[**IOCTL\_BTH\_SDP\_DISCONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)

[**IOCTL\_BTH\_SDP\_REMOVE\_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)

[**IOCTL\_BTH\_SDP\_SERVICE\_ATTRIBUTE\_SEARCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)

[**IOCTL\_両方\_SDP\_サービス\_検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)

[**IOCTL\_BTH\_SDP\_SUBMIT\_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)

[**IOCTL\_BTH\_SDP\_SUBMIT\_RECORD\_WITH\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)

Bluetooth ドライバー スタックは、次の Ioctl をサポートしていると[ **BRBs** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb)を介して (通常、ドライバーの通信用)、カーネル モードの呼び出し元[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control):

[**BRB\_HCI\_GET\_LOCAL\_BD\_ADDR**](https://docs.microsoft.com/previous-versions/ff536611(v=vs.85))

[**BRB\_L2CA\_登録\_サーバー**](https://docs.microsoft.com/previous-versions/ff536618(v=vs.85))

[**BRB\_L2CA\_登録解除\_サーバー**](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))

[**BRB\_L2CA\_オープン\_チャネル**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))

[**BRB\_L2CA\_オープン\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))

[**BRB\_L2CA\_閉じる\_チャネル**](https://docs.microsoft.com/previous-versions/ff536614(v=vs.85))

[**BRB\_L2CA\_ACL\_転送**](https://docs.microsoft.com/previous-versions/ff536613(v=vs.85))

[**BRB\_L2CA\_UPDATE\_チャネル**](https://docs.microsoft.com/previous-versions/ff536620(v=vs.85))

[**BRB\_L2CA\_PING**](https://docs.microsoft.com/previous-versions/ff536617(v=vs.85))

[**BRB\_登録\_PSM**](https://docs.microsoft.com/previous-versions/ff536621(v=vs.85))

[**BRB\_登録解除\_PSM**](https://docs.microsoft.com/previous-versions/ff536632(v=vs.85))

[**BRB\_SCO\_登録\_サーバー**](https://docs.microsoft.com/previous-versions/ff536628(v=vs.85))

[**BRB\_SCO\_登録解除\_サーバー**](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))

[**BRB\_SCO\_オープン\_チャネル**](https://docs.microsoft.com/previous-versions/ff536626(v=vs.85))

[**BRB\_SCO\_オープン\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))

[**BRB\_SCO\_閉じる\_チャネル**](https://docs.microsoft.com/previous-versions/ff536622(v=vs.85))

[**BRB\_SCO\_転送**](https://docs.microsoft.com/previous-versions/ff536629(v=vs.85))

[**BRB\_SCO\_取得\_チャネル\_情報**](https://docs.microsoft.com/previous-versions/ff536624(v=vs.85))

[**BRB\_SCO\_取得\_システム\_情報**](https://docs.microsoft.com/previous-versions/ff536625(v=vs.85))

[**BRB\_SCO\_フラッシュ\_チャネル**](https://docs.microsoft.com/previous-versions/ff536623(v=vs.85))

[**BRB\_ACL\_取得\_モード**](https://docs.microsoft.com/previous-versions/ff536609(v=vs.85))

[**BRB\_ACL\_ENTER\_ACTIVE\_モード**](https://docs.microsoft.com/previous-versions/ff536608(v=vs.85))

[**BRB\_取得\_デバイス\_インターフェイス\_文字列**](https://docs.microsoft.com/previous-versions/ff536610(v=vs.85))

[**IOCTL\_内部\_両方\_送信\_BRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bth_submit_brb)

[**IOCTL\_内部\_BTHENUM\_取得\_DEVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)

[**IOCTL\_内部\_BTHENUM\_取得\_ENUMINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo)

前の一覧で説明されている Ioctl を使用する方法の詳細については、次を参照してください。 [Bluetooth Ioctl](bluetooth-ioctls2.md)します。

プロファイルのドライバーでは、IOCTL 主に使用して\_内部\_両方\_送信\_BRB と通信して、Bluetooth ドライバー スタックで提供される機能と対話します。 プロファイルのドライバーは IOCTL\_内部\_両方\_送信\_BRB 可変長のデータ構造を提供するには Bluetooth 要求のブロックが呼び出されます ( [ **BRB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb))デバイスを管理します。 プロファイルのドライバーは、リモート デバイスへの接続を開いたり閉じたりして、入力と出力のほとんどのタスクを実行する BRBs を使用します。 IOCTL\_内部\_両方\_送信\_BRB には、Bluetooth の操作を実行する詳細を説明する BRB が含まれています。 構築し、Bluetooth ドライバー スタック ダウン BRBs を送信する方法の詳細については、次を参照してください。[のビルドと送信を BRB](building-and-sending-a-brb.md)します。

各 BRB がによって定義されている標準ヘッダーで始まる、 [ **BRB\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_header)構造、BRB の残りの部分の構造を決定する、BRB の型を指定します。 **型**で見つかった値のいずれかでなければなりませんメンバー、 [ **BRB\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ne-bthddi-_brb_type)列挙型では、Bluetooth 操作の種類を決定しますが、。ドライバーの要求をプロファイルします。 サイズと BRB 構造は、BRB の種類に応じて変わります。 **長さ**、BRB のメンバー\_ヘッダー構造、BRB のバイト単位のサイズを指定します。 [ **BthAllocateBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbth_allocate_brb)、 [ **BthInitializeBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbth_initialize_brb)、および[ **BthReuseBrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/nc-bthddi-pfnbth_reuse_brb)関数が自動的に設定、**型**と**長さ**メンバー。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_local_bd_addr" data-raw-source="[&lt;strong&gt;_BRB_GET_LOCAL_BD_ADDR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_local_bd_addr)"><strong>_BRB_GET_LOCAL_BD_ADDR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_register_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_register_server)"><strong>_BRB_L2CA_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_unregister_server)"><strong>_BRB_L2CA_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_close_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_close_channel)"><strong>_BRB_L2CA_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_ACL_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_acl_transfer" data-raw-source="[&lt;strong&gt;_BRB_L2CA_ACL_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_acl_transfer)"><strong>_BRB_L2CA_ACL_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_UPDATE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_update_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UPDATE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_update_channel)"><strong>_BRB_L2CA_UPDATE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_PING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_ping" data-raw-source="[&lt;strong&gt;_BRB_L2CA_PING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_l2ca_ping)"><strong>_BRB_L2CA_PING</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_REGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_UNREGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_psm)"><strong>_BRB_PSM</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_register_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_register_server)"><strong>_BRB_SCO_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_unregister_server)"><strong>_BRB_SCO_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_close_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_close_channel)"><strong>_BRB_SCO_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_transfer" data-raw-source="[&lt;strong&gt;_BRB_SCO_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_transfer)"><strong>_BRB_SCO_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_GET_CHANNEL_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_channel_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_CHANNEL_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_channel_info)"><strong>_BRB_SCO_GET_CHANNEL_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_GET_SYSTEM_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_system_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_SYSTEM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_get_system_info)"><strong>_BRB_SCO_GET_SYSTEM_INFO</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_FLUSH_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_flush_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_FLUSH_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_sco_flush_channel)"><strong>_BRB_SCO_FLUSH_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_ACL_GET_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_get_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_GET_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_get_mode)"><strong>_BRB_ACL_GET_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_ACL_ENTER_ACTIVE_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_enter_active_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_ENTER_ACTIVE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_acl_enter_active_mode)"><strong>_BRB_ACL_ENTER_ACTIVE_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_GET_DEVICE_INTERFACE_STRING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_device_interface_string" data-raw-source="[&lt;strong&gt;_BRB_GET_DEVICE_INTERFACE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_brb_get_device_interface_string)"><strong>_BRB_GET_DEVICE_INTERFACE_STRING</strong></a></p></td>
</tr>
</tbody>
</table>

 

Bluetooth の Ioctl および BRBs の使用に関する詳細については、次を参照してください。[のビルドと送信を BRB](building-and-sending-a-brb.md)します。

 

 





