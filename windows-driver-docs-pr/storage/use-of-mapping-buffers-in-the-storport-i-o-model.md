---
title: Storport I/O モデルでのマッピング バッファーの使用
description: Storport I/O モデルでのマッピング バッファーの使用
ms.assetid: cd22ec31-ff4d-42d4-a47d-7b8bd85804be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db9b2522ca2895b24f9ff8d42310980f8586594a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844437"
---
# <a name="use-of-mapping-buffers-in-the-storport-io-model"></a>Storport I/O モデルでのマッピング バッファーの使用


## <span id="ddk_use_of_mapping_buffers_in_the_storport_i_o_model_kg"></span><span id="DDK_USE_OF_MAPPING_BUFFERS_IN_THE_STORPORT_I_O_MODEL_KG"></span>


SCSI ポート i/o モデルでは、ミニポートドライバーによって、SRB i/o バッファー用にシステム仮想メモリの割り当てとマップを行うために、ポートドライバーが必要になる場合があります。 ミニポートドライバーは、ポート[ **\_構成\_情報 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)構造の**Mapbuffers**メンバーを**TRUE**に設定することによって、i/o バッファーをマップするようにポートドライバーを構成します。

ポートドライバーが**Mapbuffers**を**TRUE**に設定して構成されている場合、ミニポートドライバーが受信する各 SRB の**DataBuffer**メンバーには、i/o バッファーのシステム仮想アドレスが含まれます。 このアドレスは、システム内のすべてのプロセスのアドレス空間で有効です。 また、ミニポートドライバーは、i/o バッファーに直接アクセスできるようになります。

一方、ミニポートドライバーによって**Mapbuffers**が**FALSE**に設定されている場合、 **DataBuffer**には、ミニポートドライバーを実行するコンテキストでは必ずしも有効ではない特定のプロセスに属する仮想アドレスが含まれます。 そのため、ミニポートドライバーは、 **DataBuffer**が指すメモリ領域にアクセスできません。

Storport i/o モデルでは、DMA ベース i/o をサポートするためにミニポートドライバーが必要です。 DMA を使用する場合、システム全体の仮想アドレスを介して間接的に SRB の i/o バッファーにアクセスするためにミニポートドライバーは必要ありません。 このビューでは、Storport i/o モデルは、[**ポート\_CONFIGURATION\_INFORMATION (storport)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))の**mapbuffers**メンバーに対して異なる値のセットを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STOR_MAP_NO_BUFFERS</p></td>
<td align="left"><p>Storport ドライバーでは、どのような種類の SRB のデータバッファーもマップされません。 そのため、そのミニポートドライバーは、受け取った任意の SRBs の<strong>DataBuffer</strong>メンバーが指すデータに直接アクセスすることは<em>できません</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STOR_MAP_ALL_BUFFERS</p></td>
<td align="left"><p>この機能は現在実装されていません。 <strong>Mapbuffers</strong>メンバーにこの値が割り当てられている場合、Storport ドライバーは STOR_MAP_NON_READ_WRITE_BUFFERS されているかのように解釈します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STOR_MAP_NON_READ_WRITE_BUFFERS</p></td>
<td align="left"><p>データ転送 (読み取りおよび書き込み) 要求ではない場合、Storport ドライバーは要求のデータバッファーをマッピングします。 同様に、SRB が読み取り要求または書き込み要求に属していない場合、ミニポートドライバーは SRB 内のデータにアクセスできます。</p></td>
</tr>
</tbody>
</table>

 

 

 




