---
title: IRP_MJ_LOCK_CONTROL
description: IRP\_MJ\_ロック\_コントロール
ms.assetid: db21d779-c423-42bd-a94b-4d8c8fd1f7cb
keywords:
- IRP_MJ_LOCK_CONTROL インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_LOCK_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3a4e53698b23db795b6d6b095bef4da1ddde2fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324364"
---
# <a name="irpmjlockcontrol"></a>IRP\_MJ\_ロック\_コントロール


## <a name="when-sent"></a>送信時


IRP\_MJ\_ロック\_コントロール要求がや他のカーネル モード ドライバー I/O マネージャーとその他のオペレーティング システム コンポーネントによって送信されます。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ターゲット デバイス オブジェクトが、ファイル システムの制御デバイス オブジェクトかどうかをファイル オブジェクトをデコードする必要があります。 大文字と小文字の場合は、ファイル システム ドライバーは IRP を適切なロックの要求を処理することがなく完了します。

それ以外の場合で、要求が発行された場合ユーザー ファイルを表すハンドルを開く、ファイル システム ドライバーのマイナー関数のコードで示される操作を実行および IRP の完了する必要があります。 それ以外の場合は、ドライバーは IRP を失敗する必要があります。

次に、有効なマイナー関数コードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_LOCK</p></td>
<td align="left"><p>Microsoft Win32 と呼ばれる、ユーザー モード アプリケーションに代わって可能性があります、バイト範囲ロックの要求を示します<strong>ロック ファイル</strong>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_ALL</p></td>
<td align="left"><p>ファイルの場合、すべてのバイト範囲ロックを解除する要求を示しますファイル オブジェクトを最後の未処理のハンドルが閉じられるため、通常は。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_UNLOCK_ALL_BY_KEY</p></td>
<td align="left"><p>キーの値を指定してすべてのバイト範囲ロックを解除する要求を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_UNLOCK_SINGLE</p></td>
<td align="left"><p>Microsoft Win32 と呼ばれる、ユーザー モード アプリケーションに代わって可能性がありますの単一のバイト範囲ロックの解放の要求を示します<strong>UnlockFile</strong>関数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


ファイル システム フィルター ドライバーは、必要な処理を実行した後はスタック上に次の下位ドライバー IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP とロック制御の要求の処理に IRP スタックの場所の次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_ロック\_コントロール、使用する必要があります。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
1 つ、または、次の詳細:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SL_EXCLUSIVE_LOCK</p></td>
<td align="left"><p>このフラグが設定されている場合は、排他バイト範囲ロックが要求されます。 それ以外の場合、共有ロックが要求されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SL_FAIL_IMMEDIATELY</p></td>
<td align="left"><p>このフラグが設定されている場合、すぐに許可できない場合、ロック要求は失敗します。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_ロック\_コントロール。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
次のいずれかを指定します。

-   IRP\_MN\_LOCK
-   IRP\_MN\_UNLOCK\_ALL
-   IRP\_MN\_UNLOCK\_すべて\_BY\_キー
-   IRP\_MN\_UNLOCK\_単一

<a href="" id="irpsp--parameters-lockcontrol-byteoffset"></a>*IrpSp-&gt;Parameters.LockControl.ByteOffset*  
ロックまたはロックを解除する範囲のバイトのファイル内のバイト オフセットを開始しています。

<a href="" id="irpsp--parameters-lockcontrol-key"></a>*IrpSp-&gt;Parameters.LockControl.Key*  
バイト範囲ロックのキー。

<a href="" id="irpsp--parameters-lockcontrol-length"></a>*IrpSp-&gt;Parameters.LockControl.Length*  
長さ (バイト単位) をロックまたはロック解除するバイトの範囲。

## <a name="see-also"></a>関連項目


[**FltProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff543427)

[**FsRtlProcessFileLock**](https://msdn.microsoft.com/library/windows/hardware/ff547166)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

 

 






