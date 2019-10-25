---
title: MRxSetSdInfo ルーチン
description: TheMRxSetSdInfo ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトのセキュリティ記述子情報を設定するように要求するために、RDBSS によって呼び出されます。
ms.assetid: 2a03dde1-440c-4e59-b989-ca4b58b91f3a
keywords:
- MRxSetSdInfo ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetSdInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2c86c1dc3caacebaf233602f96254716488a371
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841072"
---
# <a name="mrxsetsdinfo-routine"></a>MRxSetSdInfo ルーチン


*MRxSetSdInfo*ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトのセキュリティ記述子情報を設定するように要求するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetSdInfo;

NTSTATUS MRxSetSdInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxSetSdInfo*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

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
<td align="left"><p>呼び出し元には、この操作に対する適切なセキュリティが不足しています。</p></td>
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
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワークアクセスが拒否されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>リモートページファイルのセキュリティ情報の設定など、要求された機能は実装されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>セキュリティ記述子の情報は、リモート共有ではサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクトのパスが見つかりませんでした。 このエラーは、NTFS ストリームオブジェクトのセキュリティ情報を設定するように要求され、リモートファイルシステムでストリームがサポートされていない場合に返されることがあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>シンボリックリンクを処理するには、再解析が必要です。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS は、 [**IRP\_MJ\_SET\_セキュリティ**](irp-mj-set-security.md)要求の受信に応答して、 *MRxSetSdInfo*への呼び出しを発行します。

*MRxSetSdInfo*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**Setsecurity. securityinformation**メンバーは、 **irpsp-&gt;Parameters. Setsecurity. securityinformation**に設定されています。

**Setsecurity. securitydescriptor**メンバーは、 **irpsp-&gt;Parameters. setsecurity. securitydescriptor**に設定されています。

<a name="requirements"></a>要件
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

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






