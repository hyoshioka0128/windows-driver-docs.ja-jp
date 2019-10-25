---
title: Bluetooth ドライバー スタックの使用方法
description: Bluetooth ドライバー スタックの使用方法
ms.assetid: c8a68c30-4cd6-4ee2-a653-7e0c1a28f4cf
keywords:
- Bluetooth WDK、ドライバースタック
- ドライバースタック WDK Bluetooth
- スタック WDK Bluetooth
- WDK Bluetooth プラグアンドプレイ
- PnP WDK Bluetooth
- Irp WDK Bluetooth
- プロファイル ドライバー WDK Bluetooth
- IOCTL_INTERNAL_BTH_SUBMIT_BRB
- Bluetooth WDK、Bluetooth 要求ブロック
- BRBs WDK
- Bluetooth 要求ブロック WDK
- IRP_MJ_DEVICE_CONTROL
- IRP_MJ_INTERNAL_DEVICE_CONTROL
- Bluetooth WDK、Ioctl
- Ioctl WDK Bluetooth
- リモート接続 WDK Bluetooth
- 接続 WDK Bluetooth
ms.date: 07/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82a2b47ccee646e5136fa4dd414e0c083141fd14
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834505"
---
# <a name="how-to-use-the-bluetooth-driver-stack"></a>Bluetooth ドライバー スタックの使用方法


Windows が Bluetooth ドライバースタックを読み込んで初期化した後、ドライバースタックは既にペアリングされているアクティブな Bluetooth デバイスを検出します。 ドライバースタックは、すべてのペアリングされたデバイスのデバイス識別子 (デバイス Id) を生成します。 次に、ドライバースタックは標準のプラグアンドプレイ (PnP) メカニズムを使用して、各デバイスに適切なプロファイルドライバーを読み込みます。 読み込まれるプロファイルドライバーは、デバイス識別子をインストールする INF ファイルに基づいて選択されます。このファイルは、bluetooth ドライバースタックによって生成され、「 [Bluetooth デバイスのインストール](installing-a-bluetooth-device.md)」で説明されています。

プロファイルドライバーは、WDM アーキテクチャに基づいたすべてのドライバーによって使用される標準の i/o 要求パケット (IRP) ベースのメカニズムを通じて、Bluetooth ドライバースタックと通信します。 プロファイルドライバーは、デバイスとの通信を行います。これは、Irp を割り当てて bluetooth ドライバースタックから Bluetooth ポートドライバー *Bthport*に送信することによって行われます。

プロファイルドライバーは、 *Bthport*によって処理される irp を割り当て、初期化します。 その後、プロファイルドライバーは、 [**irp\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)または[**irp\_MJ\_デバイスによってデバイスに配信される IOCTL 要求を使用して、デバイスと通信し\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)の IRP。 プロファイルドライバーは、IRP の次の一覧にある i/o 制御コードの1つを指定します。

Bluetooth ドライバースタックでは、 [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)によって、カーネルモードの呼び出し元に対して次の ioctl がサポートされています。

[**IOCTL\_BTH\_\_デバイスの切断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_disconnect_device)

[**IOCTL\_BTH\_\_デバイス\_情報を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_device_info)

[**IOCTL\_BTH\_\_ローカル\_情報を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_local_info)

[**IOCTL\_BTH\_\_ラジオ\_情報を取得します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_get_radio_info)

[**IOCTL\_BTH\_SDP\_属性\_検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_attribute_search)

[**IOCTL\_BTH\_SDP\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_connect)

[**IOCTL\_BTH\_SDP\_切断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_disconnect)

[**IOCTL\_BTH\_SDP\_\_レコードの削除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_remove_record)

[**IOCTL\_BTH\_SDP\_サービス\_属性\_検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_attribute_search)

[**IOCTL\_BTH\_SDP\_サービス\_検索**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_service_search)

[**IOCTL\_BTH\_SDP\_送信\_レコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)

[**IOCTL\_BTH\_SDP\_\_レコード\_を\_情報と共に送信します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record_with_info)

Bluetooth ドライバースタックは、 [**IRP\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)を使用して、次の Ioctl および[**brbs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb)カーネルモードの呼び出し元 (通常はドライバーからドライバーへの通信) をサポートしています。

[**BRB\_HCI\_\_ローカル\_BD\_ADDR を取得する**](https://docs.microsoft.com/previous-versions/ff536611(v=vs.85))

[**BRB\_L2CA\_登録\_サーバー**](https://docs.microsoft.com/previous-versions/ff536618(v=vs.85))

[**BRB\_L2CA\_\_サーバーの登録解除**](https://docs.microsoft.com/previous-versions/ff536619(v=vs.85))

[**BRB\_L2CA\_オープン\_チャネル**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))

[**BRB\_L2CA\_オープン\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536616(v=vs.85))

[**BRB\_L2CA\_\_チャネルを閉じる**](https://docs.microsoft.com/previous-versions/ff536614(v=vs.85))

[**BRB\_L2CA\_ACL\_転送**](https://docs.microsoft.com/previous-versions/ff536613(v=vs.85))

[**BRB\_L2CA\_更新\_チャネル**](https://docs.microsoft.com/previous-versions/ff536620(v=vs.85))

[**BRB\_L2CA\_PING**](https://docs.microsoft.com/previous-versions/ff536617(v=vs.85))

[**BRB\_\_PSM を登録する**](https://docs.microsoft.com/previous-versions/ff536621(v=vs.85))

[**BRB\_\_PSM の登録を解除する**](https://docs.microsoft.com/previous-versions/ff536632(v=vs.85))

[**BRB\_SCO\_\_サーバーを登録する**](https://docs.microsoft.com/previous-versions/ff536628(v=vs.85))

[**BRB\_SCO\_\_サーバーの登録解除**](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))

[**BRB\_SCO\_オープン\_チャネル**](https://docs.microsoft.com/previous-versions/ff536626(v=vs.85))

[**BRB\_SCO\_オープン\_チャネル\_応答**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))

[**BRB\_SCO\_\_チャネルを閉じる**](https://docs.microsoft.com/previous-versions/ff536622(v=vs.85))

[**BRB\_SCO\_転送**](https://docs.microsoft.com/previous-versions/ff536629(v=vs.85))

[**BRB\_SCO\_\_チャネル\_情報を取得する**](https://docs.microsoft.com/previous-versions/ff536624(v=vs.85))

[**BRB\_SCO\_\_システム\_情報を取得する**](https://docs.microsoft.com/previous-versions/ff536625(v=vs.85))

[**BRB\_SCO\_フラッシュ\_チャネル**](https://docs.microsoft.com/previous-versions/ff536623(v=vs.85))

[**BRB\_ACL\_\_モードの取得**](https://docs.microsoft.com/previous-versions/ff536609(v=vs.85))

[**BRB\_ACL\_\_アクティブ\_モードに移行する**](https://docs.microsoft.com/previous-versions/ff536608(v=vs.85))

[**BRB\_\_デバイス\_インターフェイス\_文字列を取得する**](https://docs.microsoft.com/previous-versions/ff536610(v=vs.85))

[**IOCTL\_内部\_BTH\_送信\_BRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bth_submit_brb)

[**IOCTL\_内部\_BTHENUM\_\_DEVINFO を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_devinfo)

[**IOCTL\_内部\_BTHENUM\_\_ENUMINFO を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_internal_bthenum_get_enuminfo)

前の一覧で説明した Ioctl の使用方法の詳細については、「 [Bluetooth ioctl](bluetooth-ioctls2.md)」を参照してください。

プロファイルドライバーは、主に IOCTL\_内部\_BTH\_送信\_BRB を使用して、Bluetooth ドライバースタックで提供される機能と通信し、対話します。 プロファイルドライバーは、IOCTL\_内部\_BTH\_SUBMIT\_BRB を使用して、Bluetooth 要求ブロック ( [**brb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb)) と呼ばれる可変長のデータ構造を管理対象デバイスに配信します。 プロファイルドライバーは BRBs を使用して、リモートデバイスへの接続を開いたり閉じたりし、ほとんどの入力と出力のタスクを実行します。 IOCTL\_内部\_BTH\_SUBMIT\_BRB には、実行する Bluetooth 操作をさらに説明する BRB が含まれています。 Bluetooth ドライバースタックを構築して送信する方法の詳細については、「 [brbs の構築と送信](building-and-sending-a-brb.md)」を参照してください。

各 BRB は、brb [ **\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_header)構造によって定義された標準ヘッダーで始まります。 brb の種類を指定します。これにより、brb の残りの部分の構造が決まります。 **型**のメンバーは、 [**brb\_type**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ne-bthddi-_brb_type)列挙型の値の1つと同じである必要があります。これは、プロファイルドライバーが要求する Bluetooth 操作の種類を決定します。 BRB の構造とサイズは、BRB の種類によって異なります。 BRB\_HEADER 構造体の**Length**メンバーは、brb のサイズ (バイト単位) を指定します。 [**Bthallocatebrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)、 [**bthinitializebrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_initialize_brb)の[**各関数は**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_reuse_brb)、**型**と**長さ**のメンバーを自動的に設定します。

たとえば、リモートデバイスへの接続を開くには、いずれかの関数コードを指定します。 **brb\_L2CA\_open\_channel**または brb\_SCO\_OPEN\_channel のいずれかを指定して、プロファイルドライバーが次のように設定しようとしていることを示します。リモートデバイスへの L2CAP 接続チャネルまたは SCO 接続チャネルを開きます。 Bluetooth ドライバースタックは、BRB 構造体の**status**メンバーを使用して、bluetooth 固有のステータスコードを返します。

各 BRB について、プロファイルドライバーは、実行する Bluetooth 操作に関する情報を使用して、適切な対応する構造体を割り当て、初期化する必要があります。

次の表では、プロファイルドライバーが発行できる特定の BRBs に対応する構造について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bluetooth 要求ブロック (BRB)</th>
<th align="left">対応する構造体</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BRB_HCI_GET_LOCAL_BD_ADDR</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_local_bd_addr" data-raw-source="[&lt;strong&gt;_BRB_GET_LOCAL_BD_ADDR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_local_bd_addr)"><strong>_BRB_GET_LOCAL_BD_ADDR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_register_server)"><strong>_BRB_L2CA_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_unregister_server)"><strong>_BRB_L2CA_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)"><strong>_BRB_L2CA_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_close_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_close_channel)"><strong>_BRB_L2CA_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_ACL_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_acl_transfer" data-raw-source="[&lt;strong&gt;_BRB_L2CA_ACL_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_acl_transfer)"><strong>_BRB_L2CA_ACL_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_L2CA_UPDATE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_update_channel" data-raw-source="[&lt;strong&gt;_BRB_L2CA_UPDATE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_update_channel)"><strong>_BRB_L2CA_UPDATE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_L2CA_PING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_ping" data-raw-source="[&lt;strong&gt;_BRB_L2CA_PING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_ping)"><strong>_BRB_L2CA_PING</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_REGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)"><strong>BRPSM (_M)</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_UNREGISTER_PSM</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm" data-raw-source="[&lt;strong&gt;_BRB_PSM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)"><strong>BRPSM (_M)</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_REGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_REGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_register_server)"><strong>_BRB_SCO_REGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_UNREGISTER_SERVER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_unregister_server" data-raw-source="[&lt;strong&gt;_BRB_SCO_UNREGISTER_SERVER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_unregister_server)"><strong>_BRB_SCO_UNREGISTER_SERVER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_OPEN_CHANNEL_RESPONSE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_OPEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)"><strong>_BRB_SCO_OPEN_CHANNEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_CLOSE_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_close_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_CLOSE_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_close_channel)"><strong>_BRB_SCO_CLOSE_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_TRANSFER</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_transfer" data-raw-source="[&lt;strong&gt;_BRB_SCO_TRANSFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_transfer)"><strong>_BRB_SCO_TRANSFER</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_GET_CHANNEL_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_channel_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_CHANNEL_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_channel_info)"><strong>_BRB_SCO_GET_CHANNEL_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_SCO_GET_SYSTEM_INFO</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_system_info" data-raw-source="[&lt;strong&gt;_BRB_SCO_GET_SYSTEM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_get_system_info)"><strong>_BRB_SCO_GET_SYSTEM_INFO</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_SCO_FLUSH_CHANNEL</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_flush_channel" data-raw-source="[&lt;strong&gt;_BRB_SCO_FLUSH_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_flush_channel)"><strong>_BRB_SCO_FLUSH_CHANNEL</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_ACL_GET_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_get_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_GET_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_get_mode)"><strong>_BRB_ACL_GET_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>BRB_ACL_ENTER_ACTIVE_MODE</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_enter_active_mode" data-raw-source="[&lt;strong&gt;_BRB_ACL_ENTER_ACTIVE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_acl_enter_active_mode)"><strong>_BRB_ACL_ENTER_ACTIVE_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRB_GET_DEVICE_INTERFACE_STRING</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_device_interface_string" data-raw-source="[&lt;strong&gt;_BRB_GET_DEVICE_INTERFACE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_get_device_interface_string)"><strong>_BRB_GET_DEVICE_INTERFACE_STRING</strong></a></p></td>
</tr>
</tbody>
</table>

 

Bluetooth Ioctl および BRBs の使用方法の詳細については、「 [brbs の構築と送信](building-and-sending-a-brb.md)」を参照してください。

 

 





