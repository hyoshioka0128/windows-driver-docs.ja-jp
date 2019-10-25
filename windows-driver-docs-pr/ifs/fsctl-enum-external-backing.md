---
title: FSCTL_ENUM_EXTERNAL_BACKING 制御コード
description: FSCTL\_ENUM\_外部\_バッキングコントロールコードは、バッキングソースを持つボリューム上のファイルの列挙を開始または続行します。
ms.assetid: 86B07858-2F10-48EF-AEB5-7F4A23A55F7F
keywords:
- FSCTL_ENUM_EXTERNAL_BACKING 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_ENUM_EXTERNAL_BACKING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: da606fa058d4b545d0d037d9206cad2d278c9ee8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841316"
---
# <a name="fsctl_enum_external_backing-control-code"></a>FSCTL\_ENUM\_外部\_バッキングコントロールコード


**FSCTL\_ENUM\_外部\_バッキング**コントロールコードは、バッキングソースを持つボリューム上のファイルの列挙を開始または続行します。 要求が正常に完了するたびに、バックアップされたファイルの識別子が返されます。 サポートされているすべてのファイルは、どの外部プロバイダーによってバックアップされているかに関係なく列挙されます。 連続する**FSCTL\_ENUM\_** 、ボリューム上のすべてのバックアップされたファイルを列挙するために、外部\_バックアップ要求が必要です。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 マウントを解除するボリュームを指定するファイルポインターオブジェクト。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 マウントを解除するボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作を行うには、 **FSCTL\_ENUM\_外部\_** を使用します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
なし。 を**NULL**に設定します。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
を0に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
出力バッファーへのポインター。1つ以上の**WOF\_外部\_ファイル\_ID**構造体を受け取るのに十分なサイズのサイズが必要です。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*Outputbuffer*が指す出力バッファーのサイズ。 *Outputbufferlength* &gt;= **sizeof**(WOF\_外部\_ファイル\_ID) である必要があります。

<a href="" id="lengthreturned--out-"></a>*長さが \[out を返しました\]*  
正常に完了したときに*Outputbuffer*に書き込まれるバイト数を指定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、次のいずれかの NTSTATUS 値を返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>要求元には管理者特権がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>Outputbuffer</em>によってポイントされ、 <em>outputbufferlength</em>によって指定された出力バッファーの長さが小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NO_MORE_FILES</strong></p></td>
<td align="left"><p>ボリューム上のファイルにバッキングソースが1つもありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>要求されたボリュームにアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バッキングサービスが存在しないか、開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*Outputbuffer*に返される**WOF\_外部\_ファイル\_ID**構造には、サポートされるファイルの一意のファイル識別子が含まれます。 構造体は、ntifs で次のように定義されています。

```ManagedCPlusPlus
typedef struct _WOF_EXTERNAL_FILE_ID {
    FILE_ID_128 FileId;
} WOF_EXTERNAL_FILE_ID, *PWOF_EXTERNAL_FILE_ID;
```

**外部\_バッキング要求\_FSCTL\_列挙型**は、バッキングソースを持つボリューム上の各ファイルの識別子を取得するために、連続して発行されます。 すべてのファイルが列挙されると、状態\_[\_]\_ファイルの状態コードが返されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1 更新プログラムから使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

[**FSCTL\_外部\_バッキング\_取得する**](fsctl-get-external-backing.md)

 

 






