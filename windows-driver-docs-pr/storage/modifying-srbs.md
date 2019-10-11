---
title: SRB の変更
description: SRB の変更
ms.assetid: 9077cfab-c17c-4c8e-9740-0895f227fb4b
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB の変更に関する WDK ストレージ
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 235a11afbd05d21136382cce3e0c939b88c846ca
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252465"
---
# <a name="modifying-srbs"></a>SRB の変更

前のセクションで説明したように、SCSI ミニポートドライバーの[**Driverentry**](driverentry-of-scsi-miniport-driver.md)ルーチンは、ポートドライバーが要求ごとの状態情報を保持する場合に、SRB 拡張用にメモリを割り当てるようにポートドライバーに要求する必要があります。

それ以外の場合、SCSI ミニポートドライバーは、*次の目的でのみ SRBs に* *値を書き込む*ことができます。

- **Srbstatus**メンバーと**ScsiStatus**メンバーの各操作について必要な状態を返すには

- アンダーランが発生した場合は、 **Datatransの長さ**のメンバーを更新します。

- 自動要求がサポートされている場合は、 **Senseinfobufferlength**を更新するために要求の意味の情報を転送します。

- SRB_FLAGS_UNSPECIFIED_DIRECTION が**Srbflags**メンバーで設定されていて、HBA が下位 DMA デバイスである場合は、現在の転送要求に応じて、SRB_FLAGS_DATA_IN または SRB_FLAGS_DATA_OUT をリセットします。

- ミニポートドライバーが8個以上の論理ユニットをサポートする場合は、 **lun**メンバーを論理ユニット番号に設定します。

*HwScsiFindAdapter*が[PORT_CONFIGURATION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)を設定するときに示されているように、HBA が8個を超える論理ユニットを処理できる場合、ポートドライバーは LUN 情報を解釈しません。 ミニポートドライバーは、必要に応じて、8ビット LUN を SRB アドレスから SCSI 3 アドレスにマップする役割を担います。

8ビット LUN から SCSI-3 アドレスへのマッピングは、ミニポートドライバーに固有です。 次の表は推奨マッピングを示しています。ここで、 *P*は物理アドレッシングモード、 *B*はバス、 *T*はターゲットです。

8ビット LUN

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

SCSI-3 アドレス

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

SCSI ポートドライバーは、すべての論理ユニットを示すために LUN 0xFF を予約します。
