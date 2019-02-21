---
title: FSCTL_QUERY_FILE_LAYOUT 制御コード
description: FSCTL\_クエリ\_ファイル\_レイアウト コントロールのコードをファイル システム ボリュームのファイルのレイアウト情報を取得します。
ms.assetid: C0094741-72C1-409C-89E6-BAD60A94EFD6
keywords:
- FSCTL_QUERY_FILE_LAYOUT 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: dc655d499bbf667e1b861992d5aac68a6a64aee2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559184"
---
# <a name="fsctlqueryfilelayout-control-code"></a>FSCTL\_クエリ\_ファイル\_レイアウト制御コード


FSCTL\_クエリ\_ファイル\_レイアウト コントロールのコードをファイル システム ボリュームのファイルのレイアウト情報を取得します。 この要求の結果は、ファイルのレイアウト情報のエントリのコレクションです。 返されるエントリの型包含フラグの設定によって制御されます、 [**クエリ\_ファイル\_レイアウト\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh439457)構造体。 必要に応じて、結果をフィルター処理、レイアウト情報の選択を制限するファイルのエクステントのセットが提供されることができます。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**パラメーター**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 ファイル システム ボリュームのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ファイル システム ボリュームのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 The FSCTL を使用して、\_クエリ\_ファイル\_この操作の制御コードをレイアウトします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
呼び出し元が割り当てたへのポインター [**クエリ\_ファイル\_レイアウト\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh439457)構造体。 この構造体には、選択オプションが含まれています。 省略可能なファイルのエクステントが後に含まれている**クエリ\_ファイル\_レイアウト\_入力**します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
指し示されるバッファーのバイト単位で、サイズ、 *InputBuffer*パラメーター。 サイズ*InputBuffer*以上である必要があります**sizeof**(クエリ\_ファイル\_レイアウト\_入力) + (**sizeof**(*フィルター処理*) \* (*NumberOfPairs* - 1)) ときに、 *NumberOfPairs* &gt; 0。 それ以外の場合、設定*InputBufferLength* = **sizeof**(クエリ\_ファイル\_レイアウト\_入力)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
呼び出し元が割り当てたへのポインター [**クエリ\_ファイル\_レイアウト\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh439461)構造体。 これは、このバッファーの次のファイルのレイアウトのエントリのヘッダーです。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指し示されるバッファーのバイト単位で、サイズ、 *OutputBuffer*パラメーター。 サイズ*OutputBuffer*を格納するのに十分な大きさである必要があります、 [**クエリ\_ファイル\_レイアウト\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh439461)ファイルと一緒にレイアウトとストリームのレイアウト構造が返されます。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_これらの値のいずれかなど、成功、または、適切な NTSTATUS の値します。

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
<td align="left"><p>ファイル システム ボリュームが開いているユーザーのボリュームをまたはバッファー長の値が正しいこと、または、無効なクエリ オプションが設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>呼び出し元がファイル システム ボリュームにアクセスできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p>いずれかのポインター <em>InputBuffer</em>または<em>OutputBuffer</em>が正しく整列していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>値<em>OutputBufferLength</em>ことを示します<em>OutputBuffer</em>が小さすぎてを少なくとも 1 つのレイアウトのエントリを格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p>いずれかのポインター <em>InputBuffer</em>または<em>OutputBuffer</em>が正しく整列していません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ボリュームの場合、FSCTL のすべてのレイアウト エントリを取得する\_クエリ\_ファイル\_レイアウトの要求が複数回発行される**状態\_エンド\_の\_ファイル**が返されます。 中に**状態\_成功**返されるか、呼び出し元が、FSCTL を送信を続けること\_クエリ\_ファイル\_レイアウトの残りのエントリのレイアウト要求。

レイアウトのエントリの列挙体は、含めることによって、いつでも再起動可能性があります、**クエリ\_ファイル\_レイアウト\_再起動**フラグ、**フラグ**のメンバー[**クエリ\_ファイル\_レイアウト\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh439457)します。 FSCTL 後も、\_クエリ\_ファイル\_レイアウトが返される**状態\_エンド\_の\_ファイル**、含める必要がある、**クエリ\_ファイル\_レイアウト\_再起動**次 FSCTL フラグ\_クエリ\_ファイル\_レイアウトの要求を別のレイアウトのエントリの列挙を開始します。

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
<td align="left"><p>Windows 8 以降を使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**クエリ\_ファイル\_レイアウト\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh439457)

[**クエリ\_ファイル\_レイアウト\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh439461)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






