---
title: IRP_MN_ENABLE_COLLECTION
description: 1 つまたは複数のデータを登録する任意の WMI ドライバー ブロック時間のかかる可能性があると、または収集するためのコストはこの IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: dc6c3ceb-a992-4e7b-ab25-d91c00af655a
keywords:
- IRP_MN_ENABLE_COLLECTION Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: cfe736b209065dc3575f9f9642ea0183cd4e1837
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570975"
---
# <a name="irpmnenablecollection"></a>IRP\_MN\_を有効にする\_コレクション


可能性のある時間がかかり、としてそのデータ ブロックの 1 つ以上を登録する任意の WMI ドライバーまたは*高価な*収集は、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)処理するために、 **IRP\_MN\_を有効にする\_コレクション**WMI がさらに呼び出しを要求します。ドライバーの[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI は、収集するコストがかかる要求のドライバーをドライバーに登録されているデータ ブロックのデータの蓄積を開始するには、この IRP を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**データの蓄積データ ブロックを識別する GUID を指します。

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

ドライバーでは、データ ブロックを登録 WMIREG を設定して、収集する高価なとして\_フラグ\_高コストで、**フラグ**のメンバー、 [ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)または[ **WMIGUIDREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565811)構造体。 ドライバーは、WMI を登録するときやデータ ブロックの更新プログラムをこれらの構造体を渡します。 データ収集を開始する明示的な要求を受信するまで、ドライバーはこのようなブロックのデータを収集しない必要があります。

ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、ドライバーが、ルーチンを呼び出す[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)ルーチン状態を取得または\_ドライバーは、ルーチンを定義していない場合は成功します。

ドライバーが処理する場合、 **IRP\_MN\_を有効にする\_コレクション**要求自体には、その方がよい場合にのみ**Parameters.WMI.ProviderId**同じデバイスを指しますオブジェクトに、ドライバーが渡されたポインターとして[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

要求を処理する前に、ドライバーを確認してくださいを**Parameters.WMI.DataPath**ドライバーがサポートする GUID を指します。 ドライバーが IRP が失敗する必要があり、状態を返すそうでない場合\_WMI\_GUID\_いない\_が見つかりました。 データ ブロックは有効ですが、なかった場合は、WMIREG に登録されている\_フラグ\_高コストで、ドライバーは状態を返すことができます\_成功し、さらに操作は不要です。

ブロックが有効であり WMIREG で登録されたかどうか\_フラグ\_高コストで、ドライバーは、そのデータ ブロックのすべてのインスタンスのデータ収集を有効します。

ドライバー データ ブロックのデータ収集が既に有効になっているかどうかを確認する必要はありません。 WMI では、最初のデータ コンシューマーのブロックを有効にすた後データ ブロックを有効にする 1 つの要求のみを送信します。 WMI は、その前の要求を無効にすることがなく有効にする別の要求を送信しません。

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

## <a name="see-also"></a>関連項目


[*DpWmiFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff544094)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**IRP\_MN\_DISABLE\_COLLECTION**](irp-mn-disable-collection.md)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

 

 




