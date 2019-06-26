---
title: IRP_MJ_QUERY_INFORMATION
description: ドライバーは、IRP_MJ_QUERY_INFORMATION 要求を必要に応じて処理できます。
ms.date: 08/12/2017
ms.assetid: 317f82b1-88d3-4618-9282-140eca2178b5
keywords:
- IRP_MJ_QUERY_INFORMATION カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: b4439bf7cc7596bfc2a3b2c9be1cb5b3cd6936f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382263"
---
# <a name="irpmjqueryinformation"></a>IRP\_MJ\_QUERY\_INFORMATION


ドライバーが処理できる必要に応じて、 **IRP\_MJ\_クエリ\_情報**要求。

<a name="when-sent"></a>送信時
---------

オペレーティング システムの送信、 **IRP\_MJ\_クエリ\_情報**ファイルまたはファイル ハンドルに関するメタデータを取得する要求。 たとえば、ドライバーを呼び出すと[ **ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)、オペレーティング システムの送信、 **IRP\_MJ\_クエリ\_情報**要求。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.QueryFile.FileInformationClass**メンバーは、**ファイル\_情報\_クラス**定数を提供するメタデータの型を指定します。 メタデータの種類の詳細については、次を参照してください。、 *FileInformationClass*のパラメーター、 [ **ZwQueryInformationFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)ルーチン。

**Parameters.QueryFile.Length**メンバーは、バッファーの長さを指定する、 **AssociatedIrp.SystemBuffer**へのポインターします。

## <a name="output-parameters"></a>出力パラメーター


**AssociatedIrp.SystemBuffer**ドライバーが要求された情報を提供するバッファーへのポインターします。 値**Parameters.QueryFile.FileInformationClass**メタデータの形式を決定します (、**ファイル\_*XXX*\_情報**構造) を返します。 メタデータの形式の詳細については、次を参照してください。、 [**ファイル\_情報\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_file_information_class)列挙体。

<a name="operation"></a>操作
---------

ドライバーは、この要求を処理する必要はありませんしはドライバーは、のすべての値を処理する必要はありません**Parameters.QueryFile.FileInformationClass**します。 ドライバーのディスパッチ ルーチンは、状態など、エラー コードを返す必要があります\_無効な\_デバイス\_ハンドルされない任意の値を要求します。

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


[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)

 

 




