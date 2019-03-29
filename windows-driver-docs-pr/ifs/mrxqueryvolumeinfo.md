---
title: MRxQueryVolumeInfo routine
description: MRxQueryVolumeInfo ルーチンは、ネットワーク ミニリダイレクター クエリのボリューム情報を要求できる RDBSS によって呼び出されます。
ms.assetid: 28e36992-2b6b-4484-9e7e-2cea7a2953e9
keywords:
- MRxQueryVolumeInfo ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 09d3b8389f85c7f140adc2ab86bf9d9e41386b89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582681"
---
# <a name="mrxqueryvolumeinfo-routine"></a>MRxQueryVolumeInfo routine


*MRxQueryVolumeInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがボリューム情報を照会することを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryVolumeInfo;

NTSTATUS MRxQueryVolumeInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQueryVolumeInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>呼び出し元には、この操作に適切なセキュリティが不足していました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_BUFFER_OVERFLOW</strong></td>
<td align="left"><p>ボリューム情報を受け取るバッファーが小さすぎます。</p>
<p>これは戻り値は、成功を考慮してでできるだけの非常に有効なデータとして返す必要がある、 <strong>Info.Buffer</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>要求されたデータを受信するには、バッファーが小さすぎます。</p>
<p>この値が返された場合、 <strong>InformationToReturn</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーターは、呼び出しに必要なバッファーの最小サイズを設定する必要があります成功します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。</p></td>
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
<td align="left"><p>要求された機能が実装されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

RDBSS への呼び出しを発行する*MRxQueryVolumeInfo*場合は、次のいずれかで。

-   RDBSS を受け取る、 [ **IRP\_MJ\_クエリ\_ボリューム\_情報**](irp-mj-query-volume-information.md)要求。

-   RDBSS を受け取る、 [ **IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)要求、FSCTL を\_LMR\_GET\_リンク\_追跡\_情報コントロール コード。

呼び出しの前に*MRxQueryVolumeInfo* IRP 場合\_MJ\_クエリ\_ボリューム\_RDBSS、RX では、次のメンバーを変更します情報が要求\_。によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.FsInformationClass**に設定されているメンバー **IrpSp -&gt;Parameters.QueryVolume.FsInformationClass**します。

**Info.Buffer**に設定されているメンバー **Irp -&gt;AssociatedIrp.SystemBuffer**します。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.QueryVolume.Length**します。

IRP の\_MJ\_クエリ\_ボリューム\_場合、情報を要求、 **PostRequest** 、RX のメンバー\_CONTEXT 構造は**TRUE**戻り時にから*MRxQueryVolumeInfo*、RDBSS が呼び出す[ **RxFsdPostRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff554472)要求を投稿します。 この場合、IRP\_MJ\_クエリ\_ボリューム\_情報の要求は、RX を渡す\_キュー RX に CONTEXT 構造\_ワーカー キュー、ファイル システムで処理するためにコンテキストプロセス (FSP)。

場合、 **PostRequest** 、RX のメンバー\_CONTEXT 構造は**FALSE**戻り時にから*MRxQueryVolumeInfo*ネットワークのミニ リダイレクターを設定する必要があります、**Info.LengthRemaining** 、RX のメンバー\_ボリューム情報の長さの CONTEXT 構造体が返されます。 RDBSS セット、 **IoStatus.Information**に IRP のメンバー **IrpSp -&gt;Parameters.QueryVolume.Length**マイナス、 **Info.LengthRemaining**のメンバーRX\_CONTEXT 構造体。

場合に呼び出し*MRxQueryVolumeInfo*が成功すると、ネットワークのミニ リダイレクター設定する必要があります、 **Info.LengthRemaining** 、RX のメンバー\_ための構造体、 **Info.Length**ボリューム情報の長さマイナスのメンバーが返されます。 場合に呼び出し*MRxQueryVolumeInfo*が成功した場合は、RDBSS セット、 **IoStatus.Information**に IRP のメンバー **IrpSp-&gt;Parameters.QueryVolume.Length**マイナス、 **Info.LengthRemaining** 、RX のメンバー\_CONTEXT 構造体。

IRP の\_MJ\_クエリ\_ボリューム\_情報要求、 **Info.FsInformationClass**メンバーに設定**FileFsDeviceInformation**、ネットワークのミニ リダイレクターが、RX では、次の情報を返します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.Buffer**メンバーには、ファイルが含まれる\_FS\_デバイス\_情報構造体

**Info.Buffer.Characteristics**メンバーが、ファイルを含める必要があります、ボリュームの特性に設定されている\_リモート\_オプションのいずれかとしてデバイス。

**Info.Buffer.DeviceType**にメンバーが設定されている、 **DeviceType**メンバーが関連付けられている net\_ルート構造体。 場合、**型**メンバーが関連付けられている net\_ルートは、NET\_ルート\_パイプ、 **Info.Buffer.DeviceType**メンバーがファイルに設定されている\_デバイス\_名前付き\_パイプします。

IRP の\_MJ\_クエリ\_ボリューム\_情報要求、 **Info.FsInformationClass**メンバーに設定**FileFsVolumeInformation**、ネットワークのミニ リダイレクターが、RX では、次の情報を返します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.Buffer**メンバーには、ファイルが含まれています。\_FS\_ボリューム\_情報構造体。

**Info.Buffer**にメンバーが設定されている、 **VolumeInfo**メンバーが関連付けられている net\_ルート構造体。

**Info.LengthRemaining**にメンバーが設定されている、 **VolumeInfoLength**メンバーが関連付けられている net\_ルート構造体。

*MRxQueryVolumeInfo*の RDBSS から呼び出す[ **IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)要求追跡情報のリンク。 呼び出しの前に*MRxQueryVolumeInfo* IRP の\_MJ\_ファイル\_システム\_コントロール、RX では、次のメンバーを変更する RDBSS\_CONTEXT 構造体を指すによって、 *RxContext*パラメーター。

**Info.FsInformationClass**に設定されているメンバー **FileFsObjectIdInformation**します。

**Info.Buffer**メンバーのセットをファイルに\_FS\_OBJECTID\_情報構造体。

**Info.LengthRemaining**に設定されているメンバー **sizeof**(ファイル\_FS\_OBJECTID\_情報)。

この場合、IRP の\_MJ\_ファイル\_システム\_コントロール要求、 **AssociatedIrp.SystemBuffer** IRP のメンバーがリンクを指す\_追跡\_情報構造体。

IRP として要求が開始された場合\_MJ\_ファイル\_システム\_に制御を*MRxQueryVolumeInfo*状態の戻り値を持つ\_成功または状態\_バッファー\_オーバーフロー、RDBSS コピー、 **ObjectId**ファイルのメンバー\_FS\_OBJECTID\_情報構造体が渡された、 **Info.Buffer** RX のメンバー\_ための構造体、 **NetRoot -&gt;DiskParameters.VolumeId** FCB 構造とメンバー、 **AssociatedIrp.SystemBuffer.VolumeId** IRP のメンバー。 場合に呼び出し*MRxQueryVolumeInfo*が成功した場合は、RDBSS セット、**型**リンクのメンバー\_追跡\_情報構造体。 場合、 **NetRoot -&gt;フラグ**FCB 構造体のメンバーが、NETROOT\_フラグ\_DFS\_AWARE\_NETROOT ビットが設定、**型**RDBSS によってメンバーが設定される**DfsLinkTrackingInformation**します。 場合、 **NetRoot -&gt;フラグ**FCB 構造体のメンバーには、NETROOT はありません\_フラグ\_DFS\_AWARE\_NETROOT ビットが設定、 **の種類。** に RDBSS によってメンバーが設定される**NtfsLinkTrackingInformation**します。 成功した場合、RDBSS の設定、 **IoStatus.Information**リンクのサイズに IRP のメンバー\_追跡\_情報構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxIsValidDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff550696)

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

[**RxFsdPostRequest**](https://msdn.microsoft.com/library/windows/hardware/ff554472)

 

 






