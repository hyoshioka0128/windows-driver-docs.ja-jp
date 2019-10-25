---
title: FSCTL_QUERY_RETRIEVAL_POINTERS 制御コード
description: FSCTL\_クエリ\_取得\_ポインター制御コードは、仮想クラスター番号 (VCN、ファイル/ストリーム領域内のオフセット)、論理クラスター番号 (LCN、ボリューム領域内のオフセット) の間のマッピングを取得します。InputBuffer で指定されたマップサイズまでのファイルの先頭。
ms.assetid: 463a5cb9-d4eb-42d6-9103-956b45a5abfb
keywords:
- FSCTL_QUERY_RETRIEVAL_POINTERS 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_QUERY_RETRIEVAL_POINTERS
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 517be772ac656d4a185dfbedd9a7ff7968045e60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841267"
---
# <a name="fsctl_query_retrieval_pointers-control-code"></a>FSCTL\_クエリ\_取得\_ポインター制御コード


**FSCTL\_クエリ\_取得\_ポインター**制御コードは、仮想クラスター番号 (VCN、ファイル/ストリーム領域内のオフセット)、および論理クラスター番号 (LCN、ボリューム領域内のオフセット) 間のマッピングを取得します。*InputBuffer*で指定されたマップサイズまでのファイルの先頭から開始します。

**FSCTL\_クエリ\_取得\_ポインター**は、\_[**ポインターを取得\_** ](fsctl-get-retrieval-pointers.md)取得する\_に似ています。 ただし、 **FSCTL\_クエリ\_の取得\_ポインター**は、ローカルページングファイルまたはシステムハイブのカーネルモードでのみ機能します。 ページングファイルには、ボリューム内の VCN から、基になる物理記憶域をより直接参照する LCN まで、1対1のマッピングがあることが保証されています。 FSCTL\_使用しないでください。この場合、ページファイル以外のファイルを使用した**ポインター\_ポインター\_取得**する必要があります。これは、Vcns から lcns への一対多マッピングを持つボリューム (ミラーボリュームなど) に存在する可能性があるためです。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**パラメーター**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ページングファイルまたは休止状態ファイルのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ページングファイルまたは休止状態ファイルのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 FSCTL を使用して、この操作の\_ポインターを取得\_取得\_します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
マップサイズを指定する quadlet へのポインターを格納するユーザー指定のバッファー。 マップサイズは、マップするクラスターの数です。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*の入力バッファーの長さ (バイト単位)。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
次の型の要素の配列を含むページプールメモリのバッファーへのポインター。

```cpp
struct {
 LONGLONG  SectorLengthInBytes;
 LONGLONG  StartingLogicalOffsetInBytes;
  } MappingPair;
```

この quadlet のペアの配列は、ファイルのディスク実行を定義します。 配列の最後の要素の**SectorLengthInBytes**メンバーの値が0です。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。

<a name="status-block"></a>状態ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)と[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)はどちらも STATUS\_SUCCESS または適切な NTSTATUS エラー値を返します。

<a name="remarks"></a>解説
-------

**ReFS:  **このコードはサポートされていません。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FSCTL\_取得\_ポインター\_取得する**](fsctl-get-retrieval-pointers.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






