---
title: FSCTL_FILE_LEVEL_TRIM 制御コード
description: FSCTL\_ファイル\_レベル\_トリム コントロール コード ファイル内でのデータ範囲をトリミングするメソッドを提供します。
ms.assetid: AD8A7A15-8B53-41DA-A6E4-BD1825C8CB45
keywords:
- FSCTL_FILE_LEVEL_TRIM 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_FILE_LEVEL_TRIM
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d56c4643f47d9629020aba86dc41794d152eab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365044"
---
# <a name="fsctlfileleveltrim-control-code"></a>FSCTL\_ファイル\_レベル\_トリム制御コード


**FSCTL\_ファイル\_レベル\_トリミング**コントロール コード ファイル内でのデータ範囲をトリミングするメソッドを提供します。 ファイルのトリミングの範囲は、アクセスのパフォーマンスを向上させるために、リソース組織を最適化することができます、基になるストレージ デバイスに変換されます。 **FSCTL\_ファイル\_レベル\_トリミング**要求により、仮想ディスク ファイルは解放された仮想ディスク上のデータ範囲に対応する物理記憶域をトリミング中に固定サイズで割り当てられたままにします。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 呼び出し元のポインターを不透明なインスタンス。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 マウントを解除するボリュームを指定する、ファイル ポインター オブジェクト。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 マウントを解除するボリュームのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作のコードを制御します。 使用**FSCTL\_削除\_オーバーレイ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
含める必要がありますが、入力バッファーへのポインターを**FSCTL\_ファイル\_レベル\_トリミング**構造体。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
ポインターを[**ファイル\_レベル\_トリミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)ファイルのトリミングの範囲の配列を含む構造体。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
省略可能なへのポインター [**ファイル\_レベル\_トリミング\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)トリム操作の結果を受け取る構造体。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength\[アウト\]*  
指し示されるバッファーのバイト単位のサイズ、 *OutputBuffer*パラメーター。 この値は以上である必要があります**sizeof**([**ファイル\_レベル\_トリミング\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)) 場合**ファイル\_レベル\_トリミング\_出力**に含まれている*OutputBuffer*します。 それ以外の場合、これを 0 に設定されます。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_成功または、次の値のいずれかの可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>トリムするのには、ファイルが圧縮または暗号化されて、入力または出力バッファーの長さが無効ですが、または、トリム範囲が指定されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOURCES</strong></p></td>
<td align="left"><p>内部リソース割り当てに失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>トリムの範囲は、既にロックされているバイトの範囲の一部です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>ファイルが存在するボリュームがマウントされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PURGE_FAILED</strong></p></td>
<td align="left"><p>トリムの範囲のキャッシュの消去に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NO_RANGES_PROCESSED</strong></p></td>
<td align="left"><p>トリムの範囲の配列内の範囲は処理されませんでした。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

特定の記憶域デバイスで trim を実行すると、将来の書き込みのパフォーマンスを大幅に向上させることができます。 シン プロビジョニング ストレージ システムにも割り当てプールに返しますリソースをトリミングします。 仮想ディスク上のファイルが削除されると、仮想ディスク ファイル自体のサイズは変更されません。 仮想ディスクに解放されたデータ範囲は、仮想ディスク ファイルが存在する物理ストレージには切り捨てられません。 仮想ディスクのデバイスは、ファイル システムを通知できる物理記憶域デバイスで仮想ディスク ファイル内の特定のデータ範囲をトリミングすることができます、 **FSCTL\_ファイル\_レベル\_トリミング**要求。 物理ストレージに、trim 要求をファイル システムで発行されます。 **FSCTL\_ファイル\_レベル\_トリミング**データベースやメモリのスワップ ファイルを管理するサービス アプリケーションによって要求が発行することも可能性があります。

**FSCTL\_ファイル\_レベル\_トリミング**ストレージ デバイスからファイルの選択したバイト範囲をトリミングする制御コードを試みます。 バイト範囲に含まれる、**範囲**配列、 [**ファイル\_レベル\_トリミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)構造体。 含まれる、**範囲**配列は 1 つまたは複数[**ファイル\_レベル\_トリミング\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_range)構造体。

範囲の配列に重複する範囲を含むは必ずしもエラー状態です。 これは、エクステントの処理を基になるストレージを処理する方法に依存します。

トリミングされた範囲は、ファイル システム キャッシュからページと消去されます。 倍数にトリムの範囲の長さを調整するキャッシュのページ サイズを一致させるために**ページ\_サイズ**します。 また、トリム範囲オフセットがページ境界で開始されていない場合は、次のページ境界に配置されます。 そのオフセットがページに合わせるか、長さが異なるページと、これらの制約で trim の範囲の長さを減らすことが複数のサイズを変更します。 トリムの範囲の長さは、元の長さが 2 未満のページと、オフセットがページに合わせる場合を 0 に減らすことができます。

トリムの範囲を指定する、またはページを調整ファイルの終端 (EOF) を超える、範囲は無視されます。 ただし、範囲を配置する前に EOF のオフセットがページに調整されます EOF を超えて拡張する長さを持つ複数のサイズを&lt;EOF を = です。

圧縮または暗号化されたファイルのファイル レベルのトリムはサポートされていません (を使用するファイル**属性\_フラグ\_圧縮\_マスク**または**属性\_フラグ\_ENCRYPTED**属性セット)。

ファイルの trim は任意のトランザクションの外部で実行されます。 トリム操作をロールバックすることはできません。

スパース ファイル (を使用するファイル、**属性\_フラグ\_SPARSE**属性に設定する)、ファイルの未割り当て領域でトリミングの範囲は無視されます。

含まれる場合*OutputBuffer*、 **NumRangesProcessed**のメンバー、 [**ファイル\_レベル\_トリミング\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_output)は正常に処理されたトリムの範囲の数を示します。 トリムの範囲の処理中にエラーが発生した場合**NumRangesProcessed**で終わる、残りの未処理範囲の開始インデックスを指定、 **NumRanges**のメンバー [**ファイル\_レベル\_トリミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim) - 1。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_レベル\_トリミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim)

[**ファイル\_レベル\_トリミング\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_output)

[**ファイル\_レベル\_トリミング\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_level_trim_range)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






