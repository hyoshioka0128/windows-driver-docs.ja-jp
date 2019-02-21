---
title: IRP_MN_DISABLE_COLLECTION
description: 任意の WMI ドライバーを収集する高価なとしてそのデータ ブロックの 1 つ以上を登録するには、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: de375d56-880e-4534-acab-8d0685f45ebe
keywords:
- IRP_MN_DISABLE_COLLECTION Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 4a6141a08ca3a17dcb295224f888888a3a3dd797
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531272"
---
# <a name="irpmndisablecollection"></a>IRP\_MN\_を無効にする\_コレクション


任意の WMI ドライバーを収集する高価なとしてそのデータ ブロックの 1 つ以上を登録するには、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)処理するために、 **IRP\_MN\_を無効にする\_コレクション**要求、WMI が呼び出されますドライバーの[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、累積データとして収集する高価なドライバーが登録されているデータ ブロックとどのデータ収集を有効になっているを停止するドライバーを要求するには、この IRP を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**データの蓄積を停止するか、データ ブロックを識別する GUID を指します。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_WMI\_GUID\_いない\_が見つかりました

ステータス\_無効な\_デバイス\_要求

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information**をゼロにします。

<a name="operation"></a>操作
---------

ドライバーでは、データ ブロックを登録 WMIREG を設定して、収集する高価なとして\_フラグ\_高コストで、**フラグ**のメンバー、 [ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)または[ **WMIGUIDREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565811)登録またはデータ ブロックを更新するときに、ドライバーが WMI に渡される構造体。 コレクションを有効にする明示的な要求を受信するまで、ドライバーはこのようなブロックのデータを収集しない必要があります。

ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、ドライバーが、ルーチンを呼び出す[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)ルーチン状態を取得または\_ドライバーは、ルーチンを定義していない場合は成功します。

ドライバーが処理する場合、 **IRP\_MN\_を無効にする\_コレクション**要求自体には、その方がよい場合にのみ**Parameters.WMI.ProviderId**同じデバイスを指しますオブジェクトに、ドライバーが渡されたポインターとして[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

要求を処理する前に、ドライバーを決定する必要があるかどうか**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。 データ ブロックは有効ですが、なかった場合は、WMIREG に登録されている\_フラグ\_高コストで、ドライバーは状態を返すことができます\_成功し、さらに操作は不要です。

WMI は、最後のデータ コンシューマーがそのブロックのコレクションを無効にされた場合にデータ ブロックの 1 つの無効化要求を送信するため、データ コレクションが既に無効にするかどうかを確認するドライバーの必要はありません。 WMI は、介在する要求を有効にすることがなく別の無効化要求を送信しません。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DpWmiFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff544094)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**IRP\_MN\_ENABLE\_COLLECTION**](irp-mn-enable-collection.md)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)

[**WMIGUIDREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565811)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

 

 




