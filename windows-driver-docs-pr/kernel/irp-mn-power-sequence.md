---
title: IRP_MN_POWER_SEQUENCE
description: この IRP は、デバイスの電源シーケンス値を返します。
ms.date: 08/12/2017
ms.assetid: f00c0021-a909-4d76-9114-6710e1aa4307
keywords:
- IRP_MN_POWER_SEQUENCE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 70cbc1f1ea39ecd512b4c6cce9780de7d00f6c2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828045"
---
# <a name="irp_mn_power_sequence"></a>IRP\_\_電源\_シーケンス


この IRP は、デバイスの電源シーケンス値を返します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_の電源**](irp-mj-power.md)送信時
---------

ドライバーは、この IRP を最適化として送信し、デバイスが実際に特定の電源状態を入力したかどうかを判断します。 この IRP のサポートは省略可能です。

この IRP を送信するには、ドライバーは[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)を呼び出して、irp を割り当てる必要があります。これには、主な Irp コード[**irp\_MJ\_POWER**](irp-mj-power.md)および minor irp code **IRP\_全\_の電源\_シーケンス**を指定します。 次に、ドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows Vista) または[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出して、IRP を次の下位のドライバーに渡す必要があります。 電源マネージャーは、この IRP を送信できません。

この IRP の送信者は、IRQL &lt;= ディスパッチ\_レベルで実行されている必要があります。

## <a name="input-parameters"></a>入力パラメーター


なし。

## <a name="output-parameters"></a>出力パラメーター


**Parameters。 PowerSequence**は、次のメンバーを持つ**POWER\_のシーケンス**構造を指します。

<a href="" id="sequenced1"></a>**SequenceD1**  
デバイスの電源状態が D1 以下の回数。

<a href="" id="sequenced2"></a>**SequenceD2**  
デバイスの電源状態が D2 以下になっている回数。

<a href="" id="sequenced3"></a>**SequenceD3**  
デバイスが電力状態 D3 になった回数。

シーケンス値は、デバイスが対応する電源状態または低電力状態にある最小回数を追跡します。

バスドライバーは、デバイスが対応する電源状態または低電力状態に入るたびに、 **SequenceD1**、 **SequenceD2**、 **SequenceD3**の値を少なくとも1つインクリメントします。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **irp&gt;iostatus. status**を STATUS\_SUCCESS に設定して、要求された情報が返されたことを示します。または、この irp がサポートされていないことを示すために実装\_されていない状態\_します。

<a name="operation"></a>操作
---------

この IRP は、デバイスの電源シーケンス値を返します。 バスドライバーは必要に応じて処理できます。関数とフィルタードライバーは必要に応じて送信できます。

状態の変更に時間がかかるデバイスの場合、この IRP は便利な最適化を提供します。 デバイスの電源状態が変わるたびに、バスドライバーはその電源状態のシーケンス値を増やします。 バスドライバーは、起動時にシーケンス値を初期化し、それ以降は継続的にインクリメントします。0にリセットする必要はありません。

デバイスポリシーの所有者は、デバイスをシャットダウンする前にシーケンス値を取得するためにこの IRP を1回送信し、デバイスに電力を復元するときに新しい値を取得することができます。 2つの値のセットを比較することで、ドライバーは、デバイスが実際に低電力状態に入ったかどうかを判断できます。 デバイスの電源が切断されていない場合、デバイスが D0 状態に戻ったときに、ドライバーによって時間がかかる再初期化が回避される可能性があります。

たとえば、デバイスが D2 状態に達したときに電力を復元するのに長い時間がかかる場合、ドライバーはデバイスの状態を D2 以下に設定する前に**SequenceD2**の値を格納できます。 その後、電源がデバイスに復元されるときに、ドライバーは新しい**SequenceD2**の値と格納されている値を比較して、デバイスの状態が D2 未満で実際に削除されたかどうかを判断できます。 値が一致した場合、デバイスは実際には電力状態 D2 またはそれよりも低い状態になることはなく、ドライバーはデバイスの再初期化を回避できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

 

 




