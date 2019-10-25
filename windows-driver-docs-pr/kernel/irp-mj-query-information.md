---
title: IRP_MJ_QUERY_INFORMATION
description: ドライバーは、必要に応じて IRP_MJ_QUERY_INFORMATION 要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 317f82b1-88d3-4618-9282-140eca2178b5
keywords:
- IRP_MJ_QUERY_INFORMATION カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 889fd58675427bcbd1570dbebbbcdb4a5140caa2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838603"
---
# <a name="irp_mj_query_information"></a>IRP\_MJ\_QUERY\_INFORMATION


ドライバーは、必要に応じて、 **IRP\_MJ\_クエリ\_情報**要求を処理できます。

<a name="when-sent"></a>送信時
---------

オペレーティングシステムは、 **IRP\_MJ\_QUERY\_INFORMATION**要求を送信して、ファイルまたはファイルハンドルに関するメタデータを取得します。 たとえば、ドライバーが[**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)を呼び出すと、オペレーティングシステムから**IRP\_MJ\_QUERY\_INFORMATION**要求が送信されます。

## <a name="input-parameters"></a>入力パラメーター


**パラメーター QueryFile. FileInformationClass**メンバーは、提供するメタデータの種類を指定する**ファイル\_情報\_クラス**定数です。 メタデータの種類の詳細については、 [**Zwqueryinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)ルーチンの*fileinformationclass*パラメーターを参照してください。

AssociatedIrp**メンバーは**、指定したバッファーの長さを指定します。この値は、そのメンバーが指すバッファーの長さを示します。

## <a name="output-parameters"></a>出力パラメーター


**AssociatedIrp**のメンバーは、ドライバーが要求された情報を提供するバッファーを指します。 **パラメーター**の値を指定すると、返されるメタデータ (**ファイル\_*XXX*\_情報**構造) の形式が決定されます。 メタデータの形式の詳細については、「[**ファイル\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)列挙型」を参照してください。

<a name="operation"></a>操作
---------

この要求を処理するためにドライバーは必要ありません。また、すべての可能なパラメーターの値を処理するために必要なドライバーはありません **。 QueryFile. FileInformationClass**。 ドライバーのディスパッチルーチンは、処理されないすべての値について、状態\_無効\_デバイス\_要求などのエラーコードを返す必要があります。

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


[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

 

 




