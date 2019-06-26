---
title: バグ チェック 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
description: SCSI_VERIFIER_DETECTED_VIOLATION のバグ チェックでは、0x000000F1 の値を持ちます。 これは、すべてのドライバー検証ツールの SCSI 検証違反のバグ チェック コードです。
ms.assetid: babc33f9-a467-4b19-b1a2-1898d0224d4d
keywords:
- バグ チェック 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
- SCSI_VERIFIER_DETECTED_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SCSI_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d61462de593da0eba969423d82c218a29164194f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361506"
---
# <a name="bug-check-0xf1-scsiverifierdetectedviolation"></a>バグ チェック 0xF1:SCSI\_VERIFIER\_検出\_違反


SCSI\_VERIFIER\_検出\_違反のバグ チェックが 0x000000F1 の値を持ちます。 これは、すべての Driver Verifier のバグ チェック コード**SCSI 検証**違反。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="scsiverifierdetectedviolation-parameters"></a>SCSI\_VERIFIER\_検出\_違反パラメーター


パラメーター 1 では、違反の種類を識別します。

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
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>渡される最初の引数</p></td>
<td align="left"><p>2 番目の引数が渡されます</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポート ドライバーに無効な引数が渡される<strong>ScsiPortInitialize</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1001</p></td>
<td align="left"><p>マイクロ秒の遅延</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポート ドライバーと呼ばれます<strong>ScsiPortStallExecution</strong>失速、プロセッサが長すぎる、0.1 秒を超える遅延を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1002</p></td>
<td align="left"><p>時間がかかりすぎましたルーチンのアドレス</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>(マイクロ秒)、そのルーチンの実行時間</p></td>
<td align="left"><p>ポート ドライバーと呼ばれるミニポート ルーチンは、実行する 2 番目の 0.5 よりも長くかかります。</p>
<p>(0.5 秒は、ほとんどのルーチンの上限であります。 ただし、 <strong>HwInitialize</strong>ルーチンは、5 秒間に許可し、 <strong>FindAdapter</strong>ルーチンは除外します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1003</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>SRB のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポート ドライバーでは、複数回要求を完了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1004</p></td>
<td align="left"><p>SRB のアドレス</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポート ドライバーでは、SRB 状態が無効な要求を完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1005</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>LOGICAL_UNIT_EXTENSION のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポート ドライバーと呼ばれます<strong>ScsiPortNotification</strong>を求める<strong>NextLuRequest</strong>、タグなしの要求にアクティブなままですが。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1006</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>仮想アドレスが無効です。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ミニポート ドライバーに渡された無効な仮想アドレスを<strong>ScsiPortGetPhysicalAddress</strong>します。</p>
<p>(つまり、通常、一般的なバッファー領域に指定されたアドレスがマップされない。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1007</p></td>
<td align="left"><p>ADAPTER_EXTENSION のアドレス</p></td>
<td align="left"><p>ミニポートの HW_DEVICE_EXTENSION のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>リセットの保持期間が終了すると、バスが、ミニポート ドライバーにはまだ未処理の要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p>マイクロ秒の遅延</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Storport ミニポート ドライバーと呼ばれる<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportstallexecution" data-raw-source="[StorPortStallExecution](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportstallexecution)">StorPortStallExecution</a></strong>失速プロセッサ時間の過度の長さを 0.1 秒より長い遅延を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2002 の場合</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetuncachedextension" data-raw-source="[StorPortGetUncachedExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetuncachedextension)">StorPortGetUncachedExtension</a></strong> ミニポート ドライバーからは呼び出されませんでした<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter" data-raw-source="[HwStorFindAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)">HwStorFindAdapter</a></strong>ルーチン。 <strong>StorPortGetUncachedExtension</strong>ルーチンは、ミニポート ドライバーからのみ呼び出すこと<strong>HwStorFindAdapter</strong>ルーチンとバス マスター アダプターに対してのみです。 Storport ミニポート ドライバーを設定する必要があります、 <strong>SrbExtensionSize</strong>の<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_hw_initialization_data" data-raw-source="[HW_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_hw_initialization_data)">HW_INITIALIZATION_DATA</a></strong>呼び出す前に (Storport) 構造<strong>StorPortGetUncachedExtension</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2003</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>無効なアドレスが渡された、 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase" data-raw-source="[StorPortGetDeviceBase](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase)">StorPortGetDeviceBase</a></strong>ルーチン。 <strong>StorPortGetDeviceBase</strong>ルーチンには、システムのプラグ アンド プレイ (PnP) マネージャーで、ドライバーに割り当てられているアドレスのみがサポートしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2004</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Storport ミニポート ドライバーでは、2 回以上同じ I/O 要求を完了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2005</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Storport ミニポート ドライバーでは、いずれかに無効な仮想アドレスが渡される、 <strong>StorPortRead</strong><em>xxx</em>または<strong>StorPortWrite</strong><em>xxx</em>ルーチン。 通常は、指定されたアドレスは、一般的なバッファー領域にマップされません。 指定した<em>登録</em>または<em>ポート</em>によって返されるメモリ領域の割り当てられた範囲内で指定する必要があります<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase" data-raw-source="[StorPortGetDeviceBase](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase)">StorPortGetDeviceBase</a></strong>ルーチン。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

原因の詳細については、パラメーター セクション内の各コードの説明を参照してください。

<a name="resolution"></a>解決方法
----------

このバグ チェックは、Driver Verifier が 1 つまたは複数のドライバーを監視するように指示された場合にのみ発生します。 Driver Verifier の使用は意図しない、非アクティブ化する必要があります。 この問題の原因となったドライバーの削除を検討する可能性があります。

ドライバー開発者の場合は、このバグ チェックで得られた情報を使用して、コードで、バグを修正します。

Driver Verifier **SCSI 検証**オプションは、以降 Windows XP でのみ使用できます。 Driver Verifier **Storport 検証**オプションは、以降 Windows 7 でのみ使用できます。 詳細については、Driver Verifier は、Windows ドライバー キットを参照してください。

 

 




