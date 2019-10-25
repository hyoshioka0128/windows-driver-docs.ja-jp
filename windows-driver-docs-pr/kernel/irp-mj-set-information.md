---
title: IRP_MJ_SET_INFORMATION
description: デバイスドライバーは、必要に応じて IRP_MJ_SET_INFORMATION 要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 1bcca676-2926-4d0f-9c0f-c6ea56481153
keywords:
- IRP_MJ_SET_INFORMATION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: f3406e691b4e60bf43fd5bccdcf0f5f5b40e8269
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838598"
---
# <a name="irp_mj_set_information"></a>IRP\_MJ\_SET\_INFORMATION


デバイスドライバーは、必要に応じて、 **\_情報要求\_設定する IRP\_MJ**を処理できます。

<a name="when-sent"></a>送信時
---------

オペレーティングシステムは、ファイルまたはファイルハンドルに関するメタデータを設定するために、 **IRP\_MJ\_set\_INFORMATION**要求を送信します。 たとえば、ドライバーが[**Zwsetinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)を呼び出すと、オペレーティングシステムは **\_情報要求\_設定された IRP\_MJ**を送信します。

## <a name="input-parameters"></a>入力パラメーター


**パラメーターの SetFile. FileInformationClass**メンバーは、設定するメタデータの種類を指定する**ファイル\_情報\_クラス**定数です。 メタデータの種類の詳細については、 [**Zwsetinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)の*fileinformationclass*パラメーターを参照してください。

**AssociatedIrp**メンバーは、指定したバッファーの長さを指定し**ます**。この値は、そのメンバーが指すバッファーの長さを示します。

**AssociatedIrp**は、新しい情報設定が格納されているバッファーを指します。 **パラメーター**の値によって、返されるデータの形式 (**ファイル\_*XXX*\_情報**構造) が決まります。 メタデータの形式の詳細については、「[**ファイル\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)列挙型」を参照してください。

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

この要求を処理するためにドライバーは必要ありません。また、すべての可能なパラメーターの値を処理するのに必要なドライバーはありません **。 SetFile. FileInformationClass**。 ドライバーのディスパッチルーチンは、処理されないすべての値について、状態\_無効\_デバイス\_要求などのエラーコードを返す必要があります。

[**ファイル\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)のすべての値が発生するとは限りません。

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

## <a name="see-also"></a>関連項目


[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)

 

 




