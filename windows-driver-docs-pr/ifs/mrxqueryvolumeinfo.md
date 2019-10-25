---
title: MRxQueryVolumeInfo ルーチン
description: MRxQueryVolumeInfo ルーチンは、ネットワークミニリダイレクターのクエリボリューム情報を要求するために RDBSS によって呼び出されます。
ms.assetid: 28e36992-2b6b-4484-9e7e-2cea7a2953e9
keywords:
- MRxQueryVolumeInfo ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryVolumeInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21480769e65f93c1e433ee74dfd1c3a1513c1be8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841083"
---
# <a name="mrxqueryvolumeinfo-routine"></a>MRxQueryVolumeInfo ルーチン


*MRxQueryVolumeInfo*ルーチンは、ネットワークミニリダイレクターのクエリボリューム情報を要求するために[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryVolumeInfo;

NTSTATUS MRxQueryVolumeInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQueryVolumeInfo*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターンコード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>呼び出し元には、この操作に対する適切なセキュリティが不足しています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_BUFFER_OVERFLOW</strong></td>
<td align="left"><p>ボリューム情報を受信するバッファーが小さすぎます。</p>
<p>この戻り値は成功と見なす必要があり、可能な限り多くの有効なデータが、 <em>RxContext</em>パラメーターによって示される RX_CONTEXT 構造体の<strong>情報バッファー</strong>のメンバーに返される必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>バッファーが小さすぎて要求されたデータを受け取ることができません。</p>
<p>この値が返される場合、 <em>RxContext</em>パラメーターが指す RX_CONTEXT 構造体の<strong>InformationToReturn</strong>メンバーは、呼び出しが成功するために必要なバッファーの最小サイズに設定されている必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリを完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NETWORK_NAME_DELETED</strong></td>
<td align="left"><p>ネットワーク名が削除されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>要求された機能は実装されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

RDBSS は、次のいずれかの場合に*MRxQueryVolumeInfo*の呼び出しを発行します。

-   RDBSS は、 [**IRP\_MJ\_クエリ\_ボリューム\_情報**](irp-mj-query-volume-information.md)要求を受信します。

-   RDBSS は、 [**IRP\_MJ\_ファイル\_システム\_制御**](irp-mj-file-system-control.md)要求の FSCTL\_LMR\_GET\_LINK\_情報制御コードの追跡\_を受信します。

IRP\_MJ\_クエリ\_ボリューム\_情報要求の場合に*MRxQueryVolumeInfo*を呼び出す前に、RDBSS は、 *RXCONTEXT*が指す RX\_コンテキスト構造内の次のメンバーを変更します。引き

**Info. fsinformationclass**メンバーは**irpsp-&gt;Parameters. Queryvolume. fsinformationclass**に設定されています。

**情報バッファー**のメンバーは、 **Irp-&gt;AssociatedIrp**に設定されます。

**LengthRemaining**メンバーは**irpsp-&gt;Parameters. Queryvolume. Length**に設定されています。

IRP\_MJ\_クエリ\_ボリューム\_情報要求では、RX\_コンテキスト構造の**postrequest**メンバーが*MRxQueryVolumeInfo*から返されたときに**TRUE**である場合、RDBSS はを呼び出し[**ます。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)要求をポストする RxFsdPostRequest。 この場合、IRP\_MJ\_QUERY\_VOLUME\_INFORMATION 要求は、RX\_コンテキスト構造を、ファイルシステムプロセス (FSP) による処理のためにワーカーキューに渡します。\_

*MRxQueryVolumeInfo*から返されたときに RX\_コンテキスト構造の**Postrequest**メンバーが**FALSE**の場合、ネットワークミニリダイレクターは rx\_コンテキスト構造の LengthRemaining メンバーをに設定する必要があり**ます。** 返されるボリューム情報の長さ。 RDBSS は、IRP の**Iostatus. 情報**メンバーを**irpsp-&gt;パラメーター**に設定します。 QUERYVOLUME LENGTH は RX\_CONTEXT 構造体の**LengthRemaining**メンバーを差し引いたものです。

*MRxQueryVolumeInfo*への呼び出しが成功した場合、ネットワークミニリダイレクターは、RX\_コンテキスト構造の LengthRemaining メンバーを、ボリューム情報の長さを差し引い**た値に**設定する必要があり**ます。** 結果. *MRxQueryVolumeInfo*への呼び出しが成功した場合、RDBSS は IRP の**Iostatus. 情報**メンバーを**irpsp-&gt;パラメーター**に設定します。 Queryvolume Length は\_RX の**LengthRemaining**メンバーを差し引いたものです。コンテキスト構造。

IRP\_MJ\_QUERY\_VOLUME\_INFORMATION 要求の場合、 **Info. FsInformationClass**メンバーが**FileFsDeviceInformation**に設定されていると、ネットワークミニリダイレクターは次の情報を RX に返し @no__*RxContext*パラメーターによってポイントされる t_6_ CONTEXT 構造体。\_

情報**バッファー**のメンバーには、ファイル\_FS\_デバイス\_情報構造体が含まれています

情報の. **Buffer. 特性**メンバーは、ボリュームの特性に設定されます。これには、オプションの1つとして、ファイル\_リモート\_デバイスが含まれている必要があります。

**(Devicetype**メンバーは、関連付けられている NET\_のルート構造の **(devicetype**メンバーに設定されます。 関連付けられている NET\_ルートの**Type**メンバーが NET\_ROOT\_PIPE の場合、 **(devicetype**メンバーは\_パイプという名前のファイル\_デバイス\_に設定されます。

IRP\_MJ\_QUERY\_VOLUME\_INFORMATION 要求の場合、 **Info. FsInformationClass**メンバーが**FileFsVolumeInformation**に設定されていると、ネットワークミニリダイレクターは次の情報を RX に返し @no__*RxContext*パラメーターによってポイントされる t_6_ CONTEXT 構造体。\_

情報**バッファー**のメンバーには、ファイル\_FS\_ボリューム\_情報構造体が含まれています。

**情報バッファー**のメンバーは、関連付けられている NET\_のルート構造の**volumeinfo**メンバーに設定されます。

**LengthRemaining**メンバーは、関連付けられている NET\_のルート構造の**VolumeInfoLength**メンバーに設定されます。

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)からの*MRxQueryVolumeInfo*呼び出しは、リンク追跡情報の要求です。 IRP\_MJ\_ファイル\_システム\_コントロールに対して*MRxQueryVolumeInfo*を呼び出す前に、RDBSS は、 *RxContext*パラメーターが指す RX\_CONTEXT 構造体の次のメンバーを変更します。

**FileFsObjectIdInformation**に設定された**Info. FsInformationClass**メンバー。

**情報バッファー**のメンバーは、ファイル\_FS\_OBJECTID\_情報構造体に設定されます。

**LengthRemaining**メンバーは**sizeof**(FILE\_FS\_OBJECTID\_INFORMATION) に設定されています。

この場合、IRP\_MJ\_FILE\_SYSTEM\_CONTROL 要求では、IRP の**AssociatedIrp**メンバーがリンクをポイントして\_情報構造を追跡します。\_

要求が IRP\_MJ\_ファイルとして開始された場合\_システム\_コントロールに対して、戻り値が STATUS\_SUCCESS または STATUS\_BUFFER\_OVERFLOW である*ことを示し*ます。RDBSS は、ファイルの**objectid**メンバー\_FS\_OBJECTID\_情報構造体にコピーします。これは、RX\_コンテキスト&gt;構造の情報バッファーのメンバーに渡され**ます。** **DiskParameters。** FCB 構造体のメンバーであり、IRP の**AssociatedIrp**メンバーになります。 *MRxQueryVolumeInfo*への呼び出しが成功した場合、RDBSS はリンクの**型**メンバーを\_追跡\_情報構造体に設定します。 FCB 構造体の**netroot&gt;フラグ**のメンバーが netroot\_フラグ\_DFS\_認識\_netroot ビットセットを持つ場合、**型**のメンバーは RDBSS によって**dfslinktrackinginformation**に設定されます。 FCB 構造体の**netroot&gt;フラグ**のメンバーに netroot\_フラグが設定されていない場合\_DFS\_認識\_netroot ビットセットの場合、**型**のメンバーは RDBSS によって**NtfsLinkTrackingInformation**に設定されます。 成功した場合、RDBSS は、IRP の**Iostatus. 情報**メンバーを、追跡\_情報構造\_リンクのサイズに設定します。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲットプラットフォーム</p></td>
<td align="left">デスクトップ</td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Mrx .h (Mrx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxIsValidDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

[**RxFsdPostRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)

 

 






