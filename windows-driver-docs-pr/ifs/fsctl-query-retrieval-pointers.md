---
title: FSCTL_QUERY_RETRIEVAL_POINTERS 制御コード
description: FSCTL\_クエリ\_取得\_ポインター制御コードは、仮想クラスター番号 (ために、VCN、ファイルまたはストリーム領域内のオフセット) および論理クラスター番号 (LCN、ボリュームの領域内のオフセット) 間のマッピングを取得します、。InputBuffer で指定されたマップのサイズまでファイルの先頭から始まります。
ms.assetid: 463a5cb9-d4eb-42d6-9103-956b45a5abfb
keywords:
- FSCTL_QUERY_RETRIEVAL_POINTERS は、ファイル システム ドライバーがインストール可能なコードを制御します。
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
ms.openlocfilehash: e09683e7fa5350d1546128a24f41942899783ba7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380078"
---
# <a name="fsctlqueryretrievalpointers-control-code"></a>FSCTL\_クエリ\_取得\_ポインター制御コード


**FSCTL\_クエリ\_取得\_ポインター**制御コードは、仮想クラスター番号 (ために、VCN、ファイルまたはストリーム領域内のオフセット) の間のマッピングを取得し、論理クラスター番号 (LCN、ボリュームの領域内でオフセットの) で指定されたマップのサイズの最大ファイルの先頭から始まります*InputBuffer*します。

**FSCTL\_クエリ\_取得\_ポインター**のような[ **FSCTL\_取得\_取得\_ポインター** ](fsctl-get-retrieval-pointers.md). ただし、 **FSCTL\_クエリ\_取得\_ポインター**ページング ファイルをローカルまたはシステム ハイブでカーネル モードでのみ機能します。 ページング ファイル、基になる物理記憶域を直接参照する LCN ボリューム内のために、VCN から一対一のマッピングが存在することが保証されます。 使用する必要がありますいない**FSCTL\_クエリ\_取得\_ポインター**ページング ファイル以外のファイルをミラー化されたボリュームなどのボリューム上に存在する可能性がありますのでがあるの一対多マッピングVCNs LCNs にします。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 ページング ファイルや休止状態ファイルのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ページング ファイルや休止状態ファイルのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 FSCTL を使用して、\_取得\_取得\_この操作のポインター。

<a href="" id="inputbuffer"></a>*InputBuffer*  
マップのサイズを指定する作成されますへのポインターを格納するユーザーが指定したバッファー。 マップのサイズでは、マップするクラスターの数です。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
入力バッファーの長さを (バイト単位) で*InputBuffer*します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
次の型の要素の配列を含むページ プール メモリのバッファーへのポインター。

```cpp
struct {
 LONGLONG  SectorLengthInBytes;
 LONGLONG  StartingLogicalOffsetInBytes;
  } MappingPair;
```

この作成されますペアの配列では、ファイルのディスクの実行を定義します。 値、 **SectorLengthInBytes**配列の最後の要素のメンバーは 0 になります。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指し示されるバッファーのバイト単位で、サイズ、 *OutputBuffer*パラメーター。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)と[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)状態を返す両方\_成功または適切な NTSTATUS エラー値。

<a name="remarks"></a>注釈
-------

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
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FSCTL\_取得\_取得\_ポインター**](fsctl-get-retrieval-pointers.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






