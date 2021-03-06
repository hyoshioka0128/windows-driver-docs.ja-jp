---
title: Storport I/O モデルでのマッピング バッファーの使用
description: Storport I/O モデルでのマッピング バッファーの使用
ms.assetid: cd22ec31-ff4d-42d4-a47d-7b8bd85804be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9c9399916c0c89ac76be0fabae4a367b88b7567
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386803"
---
# <a name="use-of-mapping-buffers-in-the-storport-io-model"></a>Storport I/O モデルでのマッピング バッファーの使用


## <span id="ddk_use_of_mapping_buffers_in_the_storport_i_o_model_kg"></span><span id="DDK_USE_OF_MAPPING_BUFFERS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI ポート I/O モデルでは、ミニポート ドライバーは、ポートのドライバーを割り当てたり、SRB I/O バッファーのシステムの仮想メモリをマップを要求できます。 ミニポート ドライバーが I/O バッファーを設定してマップするポートのドライバーを構成、 **MapBuffers**のメンバー、 [**ポート\_構成\_情報 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)構造体を**TRUE**します。

ポートのドライバーが構成されている場合**MapBuffers**設定**TRUE**、 **DataBuffer**ミニポート ドライバーが受信した各 SRB のメンバーには、仮想システムにが含まれますI/O バッファーのアドレス。 このアドレスは、システム内のすべてのプロセス アドレス空間では無効です。 また、ミニポート ドライバーは、I/O バッファーに直接アクセスする無料になります。

その一方で、ミニポート ドライバーが設定されている場合に**MapBuffers**に**FALSE**、 **DataBuffer**はない特定のプロセスが属している仮想アドレスが含まれますミニポート ドライバーを実行するコンテキスト内で有効とは限りません。 そのため、ミニポート ドライバーでは、メモリ領域にアクセスできません。 **DataBuffer**ポイント。

Storport の I/O モデルでは、ミニポート ドライバーが DMA ベースの I/O をサポートするために必要です。 DMA を使用する場合は、システム全体の仮想アドレスを使用しない SRB の I/O バッファーに直接アクセスするミニポート ドライバーがいけません。 このビューには、Storport の I/O モデル別のセットを定義の値、 **MapBuffers**のメンバー [**ポート\_構成\_情報 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)).

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STOR_MAP_NO_BUFFERS</p></td>
<td align="left"><p>Storport ドライバー SRB の任意の型のデータ バッファーをマップしません。 そのため、ミニポート ドライバーが必要があります<em>いない</em>によって示されるデータに直接アクセス、 <strong>DataBuffer</strong>で受信される Srb のいずれかのメンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STOR_MAP_ALL_BUFFERS</p></td>
<td align="left"><p>この機能は現在実装されていません。 場合、 <strong>MapBuffers</strong>メンバーには、この値が割り当てられている、あたかも STOR_MAP_NON_READ_WRITE_BUFFERS Storport ドライバー解釈します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STOR_MAP_NON_READ_WRITE_BUFFERS</p></td>
<td align="left"><p>Storport ドライバーでは、指定されたデータ転送 (読み取りし、書き込み) 要求は、要求は、データ バッファーがマップされます。 同様に、SRB が読み取りまたは書き込み要求に属していないこと、ミニポート ドライバーは、SRB のデータにアクセスできます。</p></td>
</tr>
</tbody>
</table>

 

 

 




