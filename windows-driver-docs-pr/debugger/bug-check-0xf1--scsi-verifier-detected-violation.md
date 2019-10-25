---
title: バグチェック 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
description: SCSI_VERIFIER_DETECTED_VIOLATION のバグチェックの値は、0x000000F1 です。 これは、すべての Driver Verifier SCSI 検証違反のバグチェックコードです。
ms.assetid: babc33f9-a467-4b19-b1a2-1898d0224d4d
keywords:
- バグチェック 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
- SCSI_VERIFIER_DETECTED_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SCSI_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ddf1055c8c72ce06884fd32897f22aea4bdc19e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827358"
---
# <a name="bug-check-0xf1-scsi_verifier_detected_violation"></a>バグチェック 0xF1: SCSI\_VERIFIER\_検出された\_違反


検出された SCSI\_検証\_ツールは\_違反バグチェックの値が0x000000F1 になっています。 これは、すべての Driver Verifier **SCSI 検証**違反のバグチェックコードです。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="scsi_verifier_detected_violation-parameters"></a>検出された SCSI\_検証\_\_違反パラメーター


パラメーター1は違反の種類を識別します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>最初の引数が渡されました</p></td>
<td align="left"><p>2番目の引数が渡されました</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポートドライバーが無効な引数を<strong>ScsiPortInitialize</strong>に渡しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1001</p></td>
<td align="left"><p>遅延 (マイクロ秒)</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポートドライバーが<strong>ScsiPortStallExecution</strong>を呼び出しましたが、0.1 秒より大きい遅延が指定されたため、プロセッサが長すぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1002</p></td>
<td align="left"><p>時間がかかりすぎるルーチンのアドレス</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>ルーチンの実行時間 (マイクロ秒)</p></td>
<td align="left"><p>ポートドライバーによって呼び出されたミニポートルーチンの実行に0.5 秒以上かかりました。</p>
<p>(0.5 秒は、ほとんどのルーチンの制限です。 ただし、 <strong>HwInitialize</strong>ルーチンは5秒間許可され、 <strong>findadapter</strong>ルーチンは除外されます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1003</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>SRB のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポートドライバーが要求を複数回完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1004</p></td>
<td align="left"><p>SRB のアドレス</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポートドライバーが、無効な SRB 状態の要求を完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1005</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>LOGICAL_UNIT_EXTENSION のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポートドライバーは<strong>ScsiPortNotification</strong>を呼び出して<strong>nextlurequest</strong>を要求しますが、タグなしの要求はアクティブのままです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1006</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>無効な仮想アドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポートドライバーが無効な仮想アドレスを<strong>ScsiPortGetPhysicalAddress</strong>に渡しました。</p>
<p>(これは通常、指定されたアドレスが共通のバッファー領域にマップされないことを意味します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1007</p></td>
<td align="left"><p>ADAPTER_EXTENSION のアドレス</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>バスのリセットホールド期間は終了しましたが、ミニポートドライバーに未処理の要求が残っています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p>遅延 (マイクロ秒)</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Storport ミニポートドライバーが<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportstallexecution" data-raw-source="[StorPortStallExecution](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportstallexecution)">Storportstallexecution</a></strong>という名前で、0.1 秒より長い遅延が発生したため、プロセッサが長時間停止しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2002</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetuncachedextension" data-raw-source="[StorPortGetUncachedExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetuncachedextension)">StorportgetHwStorFindAdapter Achedexテンション</a></strong>がミニポートドライバーの<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[HwStorFindAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"></a></strong>ルーチンから呼び出されませんでした。 <strong>StorportgetHwStorFindAdapter Achedexテンション</strong>ルーチンを呼び出すことができるのは、ミニポートドライバーのルーチンだけで、バスマスターアダプターの場合のみです。 Storport ミニポートドライバーでは、 <strong>StorportgetHW_INITIALIZATION_DATA</strong>(storport) 構造体の<strong>Srbextensionsize</strong>を設定してから、 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data" data-raw-source="[HW_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data)">storportget</a></strong>を呼び出す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2003</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase" data-raw-source="[StorPortGetDeviceBase](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)">Storportgetdevicebase</a></strong>ルーチンに無効なアドレスが渡されました。 <strong>Storportgetdevicebase</strong>ルーチンは、システムプラグアンドプレイ (PnP) マネージャーによってドライバーに割り当てられたアドレスのみをサポートしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2004</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Storport ミニポートドライバーは、同一の i/o 要求を複数回完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2005</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Storport ミニポートドライバーが、 <strong>Storportread</strong><em>Xxx</em>または<strong>StorPortWrite</strong><em>xxx</em>ルーチンの1つに無効な仮想アドレスを渡しました。 これは通常、指定されたアドレスが共通のバッファー領域にマップされないことを意味します。 指定された<em>レジスタ</em>または<em>ポート</em>は、 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase" data-raw-source="[StorPortGetDeviceBase](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)">storportgetdevicebase</a></strong>ルーチンによって返されるマップされたメモリ領域の範囲内である必要があります。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

原因の説明については、「Parameters」セクションの各コードの説明を参照してください。

<a name="resolution"></a>解像度
----------

このバグチェックは、ドライバーの検証ツールで1つ以上のドライバーを監視するように指示されている場合にのみ発生します。 ドライバーの検証ツールを使用しない場合は、非アクティブ化する必要があります。 この問題の原因となったドライバーを削除することも考えられます。

ドライバーライターの場合は、このバグチェックで取得した情報を使用して、コード内のバグを修正します。

Driver Verifier **SCSI 検証**オプションは、Windows XP 以降でのみ使用できます。 Driver Verifier **Storport 検証**オプションは、Windows 7 以降でのみ使用できます。 ドライバーの検証機能の詳細については、「Windows Driver Kit」を参照してください。

 

 




