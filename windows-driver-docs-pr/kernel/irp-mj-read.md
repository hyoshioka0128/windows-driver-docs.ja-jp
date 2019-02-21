---
title: IRP_MJ_READ
description: システムにそのデバイスからデータを転送するすべてのデバイス ドライバーには、このようなデバイス ドライバーの上層により高度なドライバーをする必要があります、DispatchRead または DispatchReadWrite ルーチン内の読み取り要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 5ae4c6c5-d8f2-4dc5-8cfd-ecb751fc88be
keywords:
- IRP_MJ_READ カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: fee47dc083df75a8e15a89a55e9563c2274c4f9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552648"
---
# <a name="irpmjread"></a>IRP\_MJ\_読み取り


システムにそのデバイスからデータを転送するすべてのデバイス ドライバーでの読み取り要求を処理する必要があります、 [ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)としてする必要があります、日常的な高度なドライバーの上層にこのようなデバイス ドライバー。

<a name="when-sent"></a>送信時
---------

いつの作成要求が正常に完了します。

場合によっては、ユーザー モード アプリケーションまたはターゲット デバイス オブジェクトを表すファイル オブジェクトのハンドルを持つ Win32 コンポーネントは、デバイスからのデータ転送を要求が。 場合によってより高度なドライバーが作成され、読み取り IRP を設定します。

## <a name="input-parameters"></a>入力パラメーター


IRP のドライバーの I/O スタックの場所に転送するバイト数を示す**Parameters.Read.Length**します。

一部のドライバーにある値を使用して、 **Parameters.Read.Key**デバイスのキューまたは Irp のドライバー管理の内部キューでは、ドライバーにより決定された順序に受信した読み取り要求を分類します。

ドライバーの特定の種類がある値を使用しても**Parameters.Read.ByteOffset**、転送操作の開始オフセットを示します。 たとえばを参照してください、 [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff549327)インストール可能なファイル システム (IFS) ドキュメントのトピックです。

## <a name="output-parameters"></a>出力パラメーター


ターゲット デバイス オブジェクトの基になるデバイス ドライバーを設定するかどうかに応じて**フラグ**か\_バッファーに格納された\_IO またはで\_直接\_のいずれかに IO、データが転送されます。次:

-   バッファー **Irp -&gt;AssociatedIrp.SystemBuffer**ドライバーがバッファー内の I/O を使用している場合。

-   MDL で説明されているバッファー **Irp -&gt;MdlAddress**基になるデバイス ドライバーがダイレクト I/O (DMA または PIO) を使用している場合。

<a name="operation"></a>操作
---------

読み取り要求の受信後より高度なドライバーは、次の下位ドライバー用の IRP で I/O スタックの場所を設定または作成し、1 つまたは複数の下位のドライバーの追加の Irp を設定します。 これを設定することができます、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) 、日常的なは入力 IRP の省略可能ですが Irp のドライバーが作成に必要な呼び出して[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679). 次に、ドライバーが要求を使用してドライバーを次の下位を渡します[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。

読み取り要求の受信後は、デバイス ドライバーは、システム メモリをそのデバイスからデータを転送します。 デバイス ドライバーのセット、**情報**IRP の完了時に I/O 状態ブロックのバイト数のフィールドが転送されます。

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


[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)

 

 




