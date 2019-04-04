---
title: IRP_MJ_SET_INFORMATION
description: デバイス ドライバーは、IRP_MJ_SET_INFORMATION 要求を必要に応じて処理できます。
ms.date: 08/12/2017
ms.assetid: 1bcca676-2926-4d0f-9c0f-c6ea56481153
keywords:
- IRP_MJ_SET_INFORMATION Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 5d9f09dae2974297c39c5b901eff114f38906e7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550163"
---
# <a name="irpmjsetinformation"></a>IRP\_MJ\_設定\_情報


デバイス ドライバーが処理できる必要に応じて、 **IRP\_MJ\_設定\_情報**要求。

<a name="when-sent"></a>送信時
---------

オペレーティング システムの送信、 **IRP\_MJ\_設定\_情報**ファイルまたはファイル ハンドルに関するメタデータを設定する要求。 たとえば、ドライバーを呼び出すと[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)、オペレーティング システムの送信、 **IRP\_MJ\_設定\_情報**要求。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.SetFile.FileInformationClass**メンバーは、**ファイル\_情報\_クラス**定数を設定するメタデータの型を指定します。 メタデータの種類の詳細については、、 *FileInformationClass*パラメーターの[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)を参照してください。

**Parameters.SetFile.Length**メンバーは、バッファーの長さを指定する、 **AssociatedIrp.SystemBuffer**へのポインターします。

**AssociatedIrp.SystemBuffer**新しい情報の設定を格納しているバッファーを指します。 値**Parameters.SetFile.FileInformationClass**データの形式を決定します (、**ファイル\_*XXX*\_情報**構造) を返します。 メタデータの形式の詳細については、次を参照してください。、 [**ファイル\_情報\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff728840)列挙体。

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ドライバーは、この要求を処理する必要はありませんしはドライバーは、のすべての値を処理する必要はありません**Parameters.SetFile.FileInformationClass**します。 ドライバーのディスパッチ ルーチンは、状態など、エラー コードを返す必要があります\_無効な\_デバイス\_ハンドルされない任意の値を要求します。

すべての有効な値の[**ファイル\_情報\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff728840)発生することができます。

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


[**ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)

 

 




