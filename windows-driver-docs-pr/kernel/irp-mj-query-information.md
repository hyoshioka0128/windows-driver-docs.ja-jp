---
title: IRP_MJ_QUERY_INFORMATION
description: ドライバーは、IRP_MJ_QUERY_INFORMATION 要求を必要に応じて処理できます。
ms.date: 08/12/2017
ms.assetid: 317f82b1-88d3-4618-9282-140eca2178b5
keywords:
- IRP_MJ_QUERY_INFORMATION カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: a9f7260d59759bf5640425cef6724c34c2c30710
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368443"
---
# <a name="irpmjqueryinformation"></a>IRP\_MJ\_QUERY\_INFORMATION


ドライバーが処理できる必要に応じて、 **IRP\_MJ\_クエリ\_情報**要求。

<a name="when-sent"></a>送信時
---------

オペレーティング システムの送信、 **IRP\_MJ\_クエリ\_情報**ファイルまたはファイル ハンドルに関するメタデータを取得する要求。 たとえば、ドライバーを呼び出すと[ **ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)、オペレーティング システムの送信、 **IRP\_MJ\_クエリ\_情報**要求。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.QueryFile.FileInformationClass**メンバーは、**ファイル\_情報\_クラス**定数を提供するメタデータの型を指定します。 メタデータの種類の詳細については、次を参照してください。、 *FileInformationClass*のパラメーター、 [ **ZwQueryInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567052)ルーチン。

**Parameters.QueryFile.Length**メンバーは、バッファーの長さを指定する、 **AssociatedIrp.SystemBuffer**へのポインターします。

## <a name="output-parameters"></a>出力パラメーター


**AssociatedIrp.SystemBuffer**ドライバーが要求された情報を提供するバッファーへのポインターします。 値**Parameters.QueryFile.FileInformationClass**メタデータの形式を決定します (、**ファイル\_*XXX*\_情報**構造) を返します。 メタデータの形式の詳細については、次を参照してください。、 [**ファイル\_情報\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff728840)列挙体。

<a name="operation"></a>操作
---------

ドライバーは、この要求を処理する必要はありませんしはドライバーは、のすべての値を処理する必要はありません**Parameters.QueryFile.FileInformationClass**します。 ドライバーのディスパッチ ルーチンは、状態など、エラー コードを返す必要があります\_無効な\_デバイス\_ハンドルされない任意の値を要求します。

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


[**ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)

 

 




