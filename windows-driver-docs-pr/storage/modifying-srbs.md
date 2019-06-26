---
title: SRB の変更
description: SRB の変更
ms.assetid: 9077cfab-c17c-4c8e-9740-0895f227fb4b
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB 変更 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd1299201e7d58474f4096c55e5246d2e8302b44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386187"
---
# <a name="modifying-srbs"></a>SRB の変更


## <span id="ddk_modifying_srbs_kg"></span><span id="DDK_MODIFYING_SRBS_KG"></span>


SCSI ミニポート ドライバーの前のセクションで説明したように[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ルーチンが、ミニポート ドライバーが、要求を保持する場合、ポートのドライバーが SRB の拡張機能のメモリを割り当てることを要求する必要があります状態情報。

SCSI ミニポート ドライバーがされる Srb に値を記述する場合は、*のみ*、次の目的と*のみ*で、次のメンバー。

-   各操作に関する必要な状態を返すため、 **SrbStatus**と**ScsiStatus**メンバー

-   更新するはアンダーランが発生した場合、 **DataTransferLength**メンバー

-   自動要求の意味をサポートし、転送要求の意味については、更新する場合、 **SenseInfoBufferLength**

-   場合 SRB\_フラグ\_未指定\_方向が設定されて、 **SrbFlags**メンバーと HBA は、SRB をリセットする、下位の DMA デバイス\_フラグ\_データ\_IN または SRB\_フラグ\_データ\_アウト、現在の転送要求に該当します。

-   ミニポート ドライバーが設定する、8 つ以上の論理ユニットをサポートしているかどうか、 **Lun**論理ユニット番号へのメンバー

HBA が 8 個を超えるの論理ユニットを処理できる場合というよう*HwScsiFindAdapter*設定、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)、ポート、ドライバーは LUN の情報を解釈しません。 ミニポート ドライバーは、必要な場合は、scsi-3 アドレスに、SRB から 8 ビットの LUN をマッピングします。

8 ビット LUN から scsi-3 アドレスへのマッピングは、ミニポート ドライバーに固有です。 次の表は、推奨されるマッピングを示します、 *P* 、物理アドレス指定モードは、 *B* 、バスと*T*はターゲットです。

8 ビット LUN

<table>
<colgroup>
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ビット/バイト</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>B</p></td>
<td align="left"><p>B</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
</tr>
</tbody>
</table>

 

Scsi-3 アドレス

<table>
<colgroup>
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ビット/バイト</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>B</p></td>
<td align="left"><p>B</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
</tr>
</tbody>
</table>

 

SCSI ポート ドライバーでは、LUN 0 xff までを示すすべての論理ユニットを予約します。

 

 




