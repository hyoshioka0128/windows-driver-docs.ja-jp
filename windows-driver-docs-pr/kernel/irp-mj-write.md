---
title: IRP_MJ_WRITE
description: システムからそのデバイスにデータを転送するすべてのデバイス ドライバーには、このようなデバイス ドライバーの上層により高度なドライバーをする必要があります、DispatchWrite または DispatchReadWrite ルーチン内の書き込み要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: d0db505e-2b3c-4b69-83ef-1a52e37e5d1a
keywords:
- IRP_MJ_WRITE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 26abfb3d0f584ed6bd637fc1975e5d7a1f34528e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532268"
---
# <a name="irpmjwrite"></a>IRP\_MJ\_書き込み


システムからそのデバイスにデータを転送するすべてのデバイス ドライバーがで書き込み要求を処理する必要があります、 [ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchread--dispatchwrite--and-dispatchreadwrite-routines)または[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchread--dispatchwrite--and-dispatchreadwrite-routines)としてする必要があります、日常的な高度なドライバーの上層にこのようなデバイス ドライバー。

<a name="when-sent"></a>送信時
---------

いつの作成要求が正常に完了します。

場合によっては、デバイスへのデータ転送は、ユーザー モード アプリケーションまたはターゲットのデバイス オブジェクトを表すファイル オブジェクトのハンドルを Win32 コンポーネントが必要です。 場合によってより高度なドライバーが作成され、書き込み IRP を設定します。

## <a name="input-parameters"></a>入力パラメーター


IRP のドライバーの I/O スタックの場所に転送するバイト数を示す**Parameters.Write.Length**します。

一部のドライバーにある値を使用して、 **Parameters.Write.Key**デバイスのキューまたは Irp のドライバー管理の内部キューでは、ドライバーにより決定された順序に書き込み要求を分類します。

ドライバーの特定の種類がある値を使用しても**Parameters.Write.ByteOffset**、転送操作の開始オフセットを示します。 たとえばを参照してください、 [ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff549427)インストール可能なファイル システム (IFS) ドキュメントのトピックです。

ターゲット デバイス オブジェクトの基になるデバイス ドライバーを設定するかどうかに応じて**フラグ**で\_バッファーに格納された\_IO またはか\_直接\_のいずれかから IO、データを転送次:

-   バッファー **Irp -&gt;AssociatedIrp.SystemBuffer**ドライバーがバッファー内の I/O を使用している場合、

-   MDL で説明されているバッファー **Irp -&gt;MdlAddress**基になるデバイス ドライバーがダイレクト I/O (DMA または PIO) を使用している場合、

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

書き込み要求の受信後より高度なドライバーは、次の下位ドライバー用の IRP で I/O スタックの場所を設定または作成し、1 つまたは複数の下位のドライバーの追加の Irp を設定します。 これを設定することができます、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) 、日常的なは入力 IRP の省略可能ですが Irp のドライバーが作成に必要な呼び出して[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679). 次に、ドライバーが要求を使用してドライバーを次の下位を渡します[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。

書き込み要求の受信後は、デバイス ドライバーは、システム メモリからそのデバイスにデータを転送します。 デバイス ドライバーのセット、**情報**IRP の完了時に I/O 状態ブロックのバイト数のフィールドが転送されます。

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


[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[*IoCompletion*](https://msdn.microsoft.com/library/windows/hardware/ff548354)

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)

 

 




