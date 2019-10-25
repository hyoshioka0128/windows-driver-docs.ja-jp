---
title: FSCTL_QUERY_FILE_LAYOUT 制御コード
description: FSCTL\_クエリ\_ファイル\_レイアウトコントロールコードは、ファイルシステムボリュームのファイルレイアウト情報を取得します。
ms.assetid: C0094741-72C1-409C-89E6-BAD60A94EFD6
keywords:
- FSCTL_QUERY_FILE_LAYOUT 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_QUERY_FILE_LAYOUT
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f508626bfb7ca07c5ca5545a7329dee5af89ce5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841290"
---
# <a name="fsctl_query_file_layout-control-code"></a>FSCTL\_クエリ\_ファイル\_レイアウトコントロールコード


FSCTL\_クエリ\_ファイル\_レイアウトコントロールコードは、ファイルシステムボリュームのファイルレイアウト情報を取得します。 この要求の結果は、ファイルレイアウト情報のエントリのコレクションです。 返されるエントリの種類は、[**クエリ\_ファイル\_レイアウト\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)構造に含めるフラグを設定することによって制御されます。 必要に応じて、一連のファイル範囲を指定して、レイアウト情報の選択を制限することで、結果をフィルター処理できます。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ファイルシステムボリュームのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ファイルシステムボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作には、FSCTL\_クエリ\_ファイル\_レイアウトコントロールコードを使用します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
呼び出し元によって割り当てられた[**クエリ\_ファイル\_レイアウト\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)構造体へのポインター。 この構造体には、選択オプションが含まれています。 **クエリ\_ファイル\_レイアウト\_入力**の後に、オプションのファイルのエクステントが含まれます。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*パラメーターが指すバッファーのサイズ (バイト単位)。 *Numberofpairs* &gt; 0 の場合、 *InputBuffer*のサイズは少なくとも**sizeof**(クエリ\_ファイル\_LAYOUT\_INPUT) + (**sizeof**(*Filter*) \* (*numberofpairs* )) である必要があります。 それ以外の場合は、 *Inputbufferlength* = **sizeof**(クエリ\_ファイル\_レイアウト\_入力) に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
呼び出し元によって割り当てられた[**クエリ\_ファイル\_レイアウト\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)構造体へのポインター。 これは、このバッファーで後に続くファイルレイアウトエントリのヘッダーです。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。 *Outputbuffer*のサイズは、返されるファイルレイアウトおよびストリームレイアウト構造と共に、 [ **\_レイアウト\_出力\_ファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)を格納するのに十分な大きさである必要があります。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、次のいずれかの値のように、STATUS\_SUCCESS または適切な NTSTATUS 値を返します。

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
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>ファイルシステムボリュームがオープンユーザーボリュームではないか、バッファー長の値が正しくないか、または無効なクエリオプションが設定されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>呼び出し元がファイルシステムボリュームにアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p><em>InputBuffer</em>または<em>outputbuffer</em>のポインターが適切にアラインされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>Outputbufferlength</em>の値は、 <em>outputbuffer</em>が少なくとも1つのレイアウトエントリを格納するには小さすぎることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><em>InputBuffer</em>または<em>outputbuffer</em>のポインターが適切にアラインされていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ボリュームのすべてのレイアウトエントリを取得するために、FSCTL\_クエリ\_ファイル\_レイアウト要求は、 **\_ファイルのステータス\_終了\_** が返されるまで複数回発行されます。 **状態\_SUCCESS**が返されますが、呼び出し元は、残りのレイアウトエントリに対して\_レイアウト要求に対して、FSCTL\_クエリ\_ファイルの送信を続行できます。

レイアウトエントリの列挙は、クエリ[ **\_ファイル\_レイアウト\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)の**Flags**メンバーに**クエリ\_ファイル\_レイアウト\_再起動**フラグを含めることによって、いつでも再起動できます。 また、FSCTL\_QUERY\_FILE\_LAYOUT が **\_ファイルの終了\_を\_** 返した後、次の FSCTL に**クエリ\_ファイル\_レイアウト\_再起動**フラグを含める必要があり @no新しいレイアウトエントリの列挙を開始するには、クエリ\_ファイル\_レイアウト要求を実行します。

**ReFS:  **このコードはサポートされていません。

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
<td align="left"><p>Windows 8 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**クエリ\_ファイル\_レイアウト\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_input)

[**クエリ\_ファイル\_レイアウト\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_query_file_layout_output)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






