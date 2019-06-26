---
title: IRP_MJ_SET_INFORMATION
description: デバイス ドライバーは、IRP_MJ_SET_INFORMATION 要求を必要に応じて処理できます。
ms.date: 08/12/2017
ms.assetid: 1bcca676-2926-4d0f-9c0f-c6ea56481153
keywords:
- IRP_MJ_SET_INFORMATION Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: e6f0ede6dfc34f9a616484d082c07fb10cabd516
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370888"
---
# <a name="irpmjsetinformation"></a>IRP\_MJ\_SET\_INFORMATION


デバイス ドライバーが処理できる必要に応じて、 **IRP\_MJ\_設定\_情報**要求。

<a name="when-sent"></a>送信時
---------

オペレーティング システムの送信、 **IRP\_MJ\_設定\_情報**ファイルまたはファイル ハンドルに関するメタデータを設定する要求。 たとえば、ドライバーを呼び出すと[ **ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)、オペレーティング システムの送信、 **IRP\_MJ\_設定\_情報**要求。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.SetFile.FileInformationClass**メンバーは、**ファイル\_情報\_クラス**定数を設定するメタデータの型を指定します。 メタデータの種類の詳細については、次を参照してください。、 *FileInformationClass*パラメーターの[ **ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)します。

**Parameters.SetFile.Length**メンバーは、バッファーの長さを指定する、 **AssociatedIrp.SystemBuffer**へのポインターします。

**AssociatedIrp.SystemBuffer**新しい情報の設定を格納しているバッファーを指します。 値**Parameters.SetFile.FileInformationClass**データの形式を決定します (、**ファイル\_*XXX*\_情報**構造) を返します。 メタデータの形式の詳細については、次を参照してください。、 [**ファイル\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_file_information_class)列挙体。

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ドライバーは、この要求を処理する必要はありませんしはドライバーは、のすべての値を処理する必要はありません**Parameters.SetFile.FileInformationClass**します。 ドライバーのディスパッチ ルーチンは、状態など、エラー コードを返す必要があります\_無効な\_デバイス\_ハンドルされない任意の値を要求します。

すべての有効な値の[**ファイル\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_file_information_class)発生することができます。

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


[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)

 

 




