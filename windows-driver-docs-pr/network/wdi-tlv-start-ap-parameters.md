---
title: WDI_TLV_START_AP_PARAMETERS
description: WDI_TLV_START_AP_PARAMETERS は、OID_WDI_TASK_START_AP のパラメーターを含む TLV です。
ms.assetid: 6791754C-9786-4BE4-9915-7333E4E0AFB8
ms.date: 07/18/2017
keywords:
- WDI_TLV_START_AP_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b71a39ca9811b03a234e3afe89598b18bf9e1eae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330430"
---
# <a name="wditlvstartapparameters"></a>WDI\_TLV\_開始\_AP\_パラメーター


WDI\_TLV\_開始\_AP\_パラメーターがのパラメーターを含む TLV [OID\_WDI\_タスク\_開始\_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964).

## <a name="tlv-type"></a>TLV 型


0xAB

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>ビーコン期間。 0 以外の場合、このパラメーターは、ビーコン間隔を指定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>DTIM 期間。 0 以外の場合、このパラメーターは、ビーコン間隔が 0 に等しい DTIM カウント フィールドを持つ TIM 要素が含まれているビーコン フレームの送信間隔の数を指定します。 この値は、ビーコン フレームの DTIM 期間フィールドで送信されます。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>このパラメーターは、dot11ExcludeUnencrypted MIB を設定します。 有効な値とは、0 および 1 です。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>このパラメーターは、デバイスが 802.11 b をサポートしているかを指定します速度。 有効な値は 0 (サポートされていません) および 1 (サポートです)。 この値が 1 に設定されている場合、アクセス ポイントは 11 b の料金を使用してに接続するクライアントを許可する必要があります。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Windows 10 バージョン 1511、WDI バージョン 1.0.10 に追加されます。
<p>このパラメーターには、従来の SoftAP クライアントが接続できるようにするかどうかを指定します。 有効な値は 0 (許可されていません) および 1 (有効です)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Windows 10 バージョン 1511、WDI バージョン 1.0.10 に追加されます。
<p>MustUseSpecifiedChannels します。 このパラメーターは、AP がで指定されたチャネルでのみ開始するかどうかを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/dn925964" data-raw-source="[OID_WDI_TASK_START_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)">OID_WDI_TASK_START_AP</a>を持つパラメーターをタスク<a href="wdi-tlv-ap-band-channel.md" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](wdi-tlv-ap-band-channel.md)"> <strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>します。 有効な値とは、0 および 1 です。 1 に設定されている場合、アジア太平洋は指定されたリストからのみ開始できます。 設定されていない場合は、一覧は、ファームウェアを選択するチャネルの推奨設定をするものでし、場合は、指定したチャネルのいずれかの AP を開始することはできません、別のチャネルを選択こと可能性があります。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_タスク\_開始\_アジア太平洋](https://msdn.microsoft.com/library/windows/hardware/dn925964)

 

 




