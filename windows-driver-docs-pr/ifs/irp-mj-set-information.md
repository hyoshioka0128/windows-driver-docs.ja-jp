---
title: IRP_MJ_SET_INFORMATION
description: IRP\_MJ\_SET\_INFORMATION
ms.assetid: cc1b539c-8d39-4f4d-93b1-ce9fcdb8c555
keywords:
- IRP_MJ_SET_INFORMATION インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_SET_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 258147f46d4cabda6bc7efea8ae2d965aec4ab74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324408"
---
# <a name="irpmjsetinformation"></a>IRP\_MJ\_SET\_INFORMATION


## <a name="when-sent"></a>送信時


IRP\_MJ\_設定\_や他のカーネル モード ドライバー情報の要求が I/O マネージャーとその他のオペレーティング システム コンポーネントによって送信されます。 送信できる、たとえば、ユーザー モード アプリケーションには、Microsoft Win32 関数が呼び出されるとなど**SetEndOfFile**カーネル モード コンポーネントが呼び出されたときまたは[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096).

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ユーザー ファイルを表しますか、ディレクトリを開くかどうかを判断する、ファイル オブジェクトをデコードする必要があります。 場合は、ファイル システム ドライバーとして適切な要求を処理し、IRP の完了する必要があります。

次の種類の情報は、ファイルとディレクトリで設定できます。

FileBasicInformation

FileDispositionInformation

FileLinkInformation (ディレクトリ階層内に作成するサイクルを許可するファイル システム) の場合

FilePositionInformation

FileRenameInformation

次の種類の情報は、ファイルにのみ設定できます。

FileAllocationInformation

FileEndOfFileInformation

FileLinkInformation (NTFS ディレクトリ階層内に作成するサイクルを許可しないなどのファイル システム) の場合

FileValidDataLengthInformation

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP とセット ファイル情報の要求の処理に IRP スタックの場所の次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
設定するファイルまたはディレクトリの情報を含む入力バッファーへのポインター。 この情報は、次の構造体のいずれかに格納されます。

[**ファイル\_割り当て\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540232)

[**ファイル\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**ファイル\_廃棄\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545765)

[**ファイル\_エンド\_の\_ファイル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545780)

[**ファイル\_リンク\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540324)

[**ファイル\_位置\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

[**ファイル\_の名前を変更\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540344)

[**ファイル\_有効\_データ\_長さ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545873)

<a href="" id="irp--iostatus"></a>*Irp -&gt;IoStatus*へのポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)に関する最終的な完了の状態および情報を受け取る、要求された操作。 詳細については、の説明を参照して、 *IoStatusBlock*パラメーターを[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)します。

<a href="" id="irpsp--fileobject"></a>*IrpSp -&gt;FileObject*に関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_設定\_情報、使用する必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp -&gt;MajorFunction* IRP を指定します\_MJ\_設定\_情報。

<a href="" id="irpsp--parameters-setfile-advanceonly"></a>*IrpSp -&gt;Parameters.SetFile.AdvanceOnly*ファイルの終わりの操作に使用するフラグ。 使用を指定します、 **EndOfFile**メンバー [**ファイル\_エンド\_の\_ファイル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545780)ときに構造体**FileInformationClass** == **FileEndOfFileInformation**します。 場合**TRUE**、設定は、ファイルの新しい有効なデータ長**EndOfFile**現在有効なデータの長さを増加している場合にのみです。 場合**FALSE**、新しいファイル サイズの設定から**EndOfFile**します。

<a href="" id="irpsp--parameters-setfile-clustercount"></a>*IrpSp -&gt;Parameters.SetFile.ClusterCount*システム用に予約されています。

<a href="" id="irpsp--parameters-setfile-deletehandle"></a>*IrpSp -&gt;Parameters.SetFile.DeleteHandle*システム用に予約されています。

<a href="" id="irpsp--parameters-setfile-fileinformationclass"></a>*IrpSp -&gt;Parameters.SetFile.FileInformationClass*ファイル用に設定する情報の種類を指定します。 次のいずれかです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllocationInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540232" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540232)"> <strong>FILE_ALLOCATION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545762" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545762)"> <strong>FILE_BASIC_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545765" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545765)"> <strong>FILE_DISPOSITION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545780" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545780)"> <strong>FILE_END_OF_FILE_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540324" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540324)"> <strong>FILE_LINK_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545848" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545848)"> <strong>FILE_POSITION_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff540344" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540344)"> <strong>FILE_RENAME_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff545873" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545873)"> <strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong> </a>ファイル。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-setfile-fileobject"></a>*IrpSp -&gt;Parameters.SetFile.FileObject*の名前を変更またはリンクの操作。 場合*Irp の&gt;AssociatedIrp.SystemBuffer -&gt;ファイル名*、完全修飾ファイル名を含む場合、または*Irp -&gt;AssociatedIrp.SystemBuffer-&gt;RootDirectory*以外**NULL**、このメンバーは、操作の対象となっているファイルの親ディレクトリのファイル オブジェクト ポインター。 それ以外の場合は**NULL**します。

<a href="" id="irpsp--parameters-setfile-length"></a>*IrpSp -&gt;Parameters.SetFile.Length*によって指し示されるバッファーの長さをバイト単位で*Irp -&gt;AssociatedIrp.SystemBuffer*します。

<a href="" id="irpsp--parameters-setfile-replaceifexists"></a>*IrpSp -&gt;Parameters.SetFile.ReplaceIfExists*設定**TRUE**ことと同じ名前のファイルが既に存在する場合、指定されたファイルに置き換える必要がそれを指定します。 設定**FALSE**指定した名前のファイルが既に存在する場合、名前の変更操作が失敗する必要があります。

<a name="remarks"></a>注釈
-------

**AdvanceOnly**に設定されているメンバー **TRUE**を現在の有効なデータの長さをディスク上に新しい有効なデータ長に進み、ファイル システムに通知する、キャッシュ マネージャーによって**EndOfFile**. 場合**AdvanceOnly**は**FALSE**、新しいファイル サイズで、 **EndOfFile**現在のファイル サイズよりも大きくなることができます、メンバーが設定されています。

## <a name="see-also"></a>関連項目


[**ファイル\_割り当て\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540232)

[**ファイル\_BASIC\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545762)

[**ファイル\_廃棄\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545765)

[**ファイル\_エンド\_の\_ファイル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545780)

[**ファイル\_リンク\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540324)

[**ファイル\_位置\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545848)

[**ファイル\_の名前を変更\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540344)

[**ファイル\_有効\_データ\_長さ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545873)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)

 

 






