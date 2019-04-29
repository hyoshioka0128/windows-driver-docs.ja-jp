---
title: IRP_MN_POWER_SEQUENCE
description: この IRP では、デバイスの電源のシーケンス値を返します。
ms.date: 08/12/2017
ms.assetid: f00c0021-a909-4d76-9114-6710e1aa4307
keywords:
- IRP_MN_POWER_SEQUENCE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 827976878f8f947d00a9b96c78654108f662ecb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391969"
---
# <a name="irpmnpowersequence"></a>IRP\_MN\_POWER\_シーケンス


この IRP では、デバイスの電源のシーケンス値を返します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_POWER** ](irp-mj-power.md)送信されるときに
---------

ドライバーは、そのデバイスが特定の電源状態を実際に入力されたかどうかを判断するよう最適化として、この IRP を送信します。 この IRP のサポートは、省略可能です。

この IRP を送信するドライバーを呼び出す必要があります[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)を主要な IRP のコードを指定する、IRP を割り当てる[ **IRP\_MJ\_POWER**](irp-mj-power.md)と IRP コードの軽微な**IRP\_MN\_POWER\_シーケンス**します。 ドライバーは呼び出す必要がありますし、 [**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) (Windows Vista) または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) (の Windows Server 2003、Windows XP、および Windows 2000) [次へ] の下位のドライバーに IRP を渡す。 電源マネージャーは、この IRP を送信できません。

この IRP の送信者は IRQL で実行する必要があります&lt;= ディスパッチ\_レベル。

## <a name="input-parameters"></a>入力パラメーター


なし。

## <a name="output-parameters"></a>出力パラメーター


**Parameters.PowerSequence**を指す、 **POWER\_シーケンス**次のメンバーを含む構造体。

<a href="" id="sequenced1"></a>**SequenceD1**  
デバイスが D1 またはそれ以下の電源状態であった時間数。

<a href="" id="sequenced2"></a>**SequenceD2**  
デバイスが D2 またはそれ以下の電源状態であった時間数。

<a href="" id="sequenced3"></a>**SequenceD3**  
デバイスが D3 の電源状態であった時間数。

シーケンス値は、デバイスが対応する電源状態または低電力状態にあった時間の最小数を追跡します。

バス ドライバーの値をインクリメントする**SequenceD1**、 **SequenceD2**、および**SequenceD3**デバイスが対応する電源状態または低には、少なくとも毎回電源の状態。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp の&gt;IoStatus.Status**ステータス\_を要求された情報が返されることを示すために成功またはステータス\_いない\_実装されていることを示すこの IRP をサポートしません。

<a name="operation"></a>操作
---------

この IRP では、デバイスの電源のシーケンス値を返します。 バス ドライバーが必要に応じて処理します。関数とフィルター ドライバーは、必要に応じてに送信できます。

デバイスの状態を変更する時間が長い場合は、この IRP は有効な最適化を提供します。 デバイスに電源状態が変更されるたび、バス ドライバーは、その電源状態のシーケンス値をインクリメントします。 バス ドライバーがブート時に、シーケンス値を初期化し、それ以降は継続的に増加0 にリセットする必要がありますされません。

デバイスのポリシー所有者は、デバイスの電源をシャット ダウンする前に、シーケンス値を取得して、デバイスに電源を復元する場合は、新しい値を取得するもう一度この IRP を 1 回送信できます。 2 つの値のセットを比較すると、ドライバーは、デバイスが低電力状態を実際に入力されたかどうかを判断できます。 デバイスでは、電源は失われませんでした、D0 状態に戻ると、デバイス、ドライバーは、時間のかかる再初期化を回避できます。

などの場合は、デバイス D2 状態に達すると、電源を復旧する時間がかかる、ドライバー格納できる、 **SequenceD2** D2 状態または低のデバイスを設定する前に、の値します。 後で、デバイスに電源が復旧されるときに、ドライバーを比較できる新しい**SequenceD2**デバイスの状態が実際に D2 下にドロップするかどうかを判断する格納されている値を持つ値。 値が一致した場合は、デバイス実際に入力しなかった D2 の電源状態または低の状態と、ドライバーがデバイスを再初期化を回避することができます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

 

 




