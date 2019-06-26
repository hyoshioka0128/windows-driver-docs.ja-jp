---
title: FSCTL_GET_RETRIEVAL_POINTERS 制御コード
description: FSCTL\_取得\_取得\_ポインター制御コードは、特定のファイルのディスクの割り当てと場所を記述する可変サイズのデータ構造を取得します。
ms.assetid: d77790c8-9fe6-4b36-995e-40a7ea54c18a
keywords:
- FSCTL_GET_RETRIEVAL_POINTERS は、ファイル システム ドライバーがインストール可能なコードを制御します。
topic_type:
- apiref
api_name:
- FSCTL_GET_RETRIEVAL_POINTERS
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b500a5ba4094de7de16dd26f8b90a5df9e764122
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365024"
---
# <a name="fsctlgetretrievalpointers-control-code"></a>FSCTL\_取得\_取得\_ポインター制御コード


**FSCTL\_取得\_取得\_ポインター**制御コードは、特定のファイルのディスクの割り当てと場所を記述する可変サイズのデータ構造を取得します。 構造体には、仮想クラスター番号 (ために、VCN、ファイルまたはストリーム領域内のオフセット) および論理クラスター番号 (LCN、ボリュームの領域内のオフセット) 間のマッピングについて説明します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

再解析ポイントと FSCTL の詳細については\_取得\_取得\_ポインター制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 代替ストリーム、ファイル、またはどの FSCTL のディレクトリのファイル オブジェクト ポインター\_取得\_取得\_ポインターは、マッピングを取得します。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 代替ストリーム、ファイル、またはどの FSCTL のディレクトリのファイル ハンドル\_取得\_取得\_ポインターは、マッピングを取得します。 場合の値*FileHandle* VCNs と不良クラスターのファイルのエクステントのマップ、ルーチンを返します、ボリューム全体のハンドルです。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 FSCTL を使用して、\_取得\_取得\_この操作へのポインター。

<a href="" id="inputbuffer"></a>*InputBuffer*  
ポインターを開始する\_ために、VCN\_入力\_代替ストリーム、ファイル、またはディレクトリの先頭を示す仮想クラスター数 (ために、VCN) を示すバッファーの構造体。 開始\_ために、VCN\_入力\_バッファーの構造は次のように定義されます。

```cpp
typedef struct {
  LARGE_INTEGER  ;
} STARTING_VCN_INPUT_BUFFER, *PSTARTING_VCN_INPUT_BUFFER;
```

**メンバー**

<a href="" id="startingvcn"></a>**StartingVcn**  
ために、どの FSCTL で VCN\_取得\_取得\_ポインターは、エクステントおよび関連付けられている仮想と論理クラスター番号の列挙を開始します。 最初の呼び出しで[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ファイルのシステム コントロールのコードは FSCTL\_取得\_取得\_ポインター、 **StartingVcn** 0 に設定する必要があります。

場合*OutputBuffer*が十分に大きくない VCNs とファイルのエクステントのマップ全体を保持するために、呼び出し元する必要がありますより多くのマップ データを使用して要求で返される値、 **NextVcn**取得のメンバー\_ポインター\_のために、開始、VCN として、バッファーの構造体。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
入力バッファーの長さを (バイト単位) で*InputBuffer です。*

<a href="" id="outputbuffer"></a>*OutputBuffer*  
型の取得の可変サイズの構造体へのポインター\_ポインター\_代替ストリーム、ファイル、またはディレクトリに対応するディスクのエクステントの列挙を格納するバッファー。

```cpp
typedef struct RETRIEVAL_POINTERS_BUFFER {
 ULONG  ExtentCount;
  LARGE_INTEGER  StartingVcn;
 struct {
    LARGE_INTEGER  NextVcn;
    LARGE_INTEGER  Lcn;
  } Extents[1];
} RETRIEVAL_POINTERS_BUFFER, *PRETRIEVAL_POINTERS_BUFFER;
```

**メンバー**

<a href="" id="extentcount"></a>**ExtentCount**  
内の要素の数、**エクステント**配列。

<a href="" id="startingvcn"></a>**StartingVcn**  
開始のために、VCN は、関数呼び出しによって返されます。 これは必ずしも関数の呼び出しによって要求されたために、VCN のように、ファイル システム ドライバーがために、ため、要求されたに開始、VCN が掲載されている範囲の最初の VCN に切り捨てることがあります。

<a href="" id="extents-"></a>**エクステント**   
エクステント構造体の配列。 配列のメンバーの数を参照してください。 **ExtentCount**します。 配列の各メンバーは、次のメンバーがあります。

<a href="" id="nextvcn"></a>**NextVcn**  
ために、VCN [次へ] の範囲が開始されます。 いずれかから引いた値**StartingVcn** (最初の**エクステント**配列メンバー)、または**NextVcn**配列の前のメンバーの (他のすべての**エクステント**配列のメンバー) がクラスターでは、現在の範囲の長さ。

<a href="" id="lcn"></a>**Lcn**  
ボリュームの現在の範囲が開始される LCN します。 NTFS では、値 (LONGLONG)-1 は、部分的に割り当てられている圧縮単位またはスパース ファイルの未割り当て領域のいずれかを示します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指し示されるバッファーのバイト単位のサイズ、 *OutputBuffer*パラメーター。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)と[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)状態を返す両方\_成功または適切な NTSTATUS エラー値。

場合のために、VCN エクステント マップが適合しない/ *OutputBuffer*、2 つのルーチンは、状態の値を返す\_バッファー\_オーバーフロー、および呼び出し元に返される値を使用して複数のマップ データを要求する必要があります、 **NextVcn**メンバー取得の\_ポインター\_ために、開始、VCN とバッファーの構造 (**StartingVcn**) には、次の呼び出しで[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)します。

場合に指定されている値**StartingVcn**がステータス、ファイルの末尾を越える\_エンド\_の\_ファイルが返されます。

<a name="remarks"></a>注釈
-------

**FSCTL\_取得\_取得\_ポインター**制御コードは、FastFAT および exFAT のデバイスで使用できます。 この機能は、フラッシュ ドライブなどのデバイス用の BitLocker の使用をサポートします。

<a name="requirements"></a>必要条件
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

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






