---
title: FSCTL_FILE_LEVEL_TRIM 制御コード
description: FSCTL\_FILE\_LEVEL\_TRIM コントロールコードには、ファイル内のデータ範囲をトリミングするためのメソッドが用意されています。
ms.assetid: AD8A7A15-8B53-41DA-A6E4-BD1825C8CB45
keywords:
- FSCTL_FILE_LEVEL_TRIM 制御コードのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 86ddb803ece874a8a1b4c386510214329106523e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841318"
---
# <a name="fsctl_file_level_trim-control-code"></a>FSCTL\_FILE\_LEVEL\_TRIM control code


**FSCTL\_file\_LEVEL\_trim**コントロールコードには、ファイル内のデータ範囲をトリミングするためのメソッドが用意されています。 ファイルのトリミング範囲は、基になるストレージデバイスに変換されます。これにより、リソースの組織を最適化し、アクセスのパフォーマンスを向上させることができます。 **FSCTL\_FILE\_LEVEL\_TRIM**要求を使用すると、仮想ディスク上で解放されたデータ範囲に対応するために物理記憶域をトリミングしながら、仮想ディスクファイルを固定サイズで割り当てたままにすることができます。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**パラメーター**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 マウントを解除するボリュームを指定するファイルポインターオブジェクト。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 マウントを解除するボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作には、FSCTL\_使用して **\_オーバーレイを削除**してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
**FSCTL\_ファイル\_LEVEL\_TRIM**構造体を含む必要がある入力バッファーへのポインター。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
ファイルのトリム範囲の配列を含む[**trim 構造\_ファイル\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)へのポインター。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
省略可能な[**ファイル\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)へのポインター\_trim 操作の結果を受け取る出力構造を\_します。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[out\]*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。 **ファイル\_レベル\_trim\_出力**が*outputbuffer*に含まれる場合、この値は少なくとも**sizeof**([**ファイル\_レベル\_trim\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)) である必要があります。 それ以外の場合は0に設定されます。

<a name="status-block"></a>状態ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**ZWFSCONTROLFILE**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、STATUS\_SUCCESS または次のいずれかの値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">期間</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>トリミングするファイルが圧縮または暗号化されているか、入力バッファーまたは出力バッファーの長さが無効であるか、またはトリム範囲が指定されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOURCES</strong></p></td>
<td align="left"><p>内部リソースの割り当てに失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>トリム範囲は、以前にロックされていたバイト範囲の一部です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>ファイルが存在するボリュームがマウントされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PURGE_FAILED</strong></p></td>
<td align="left"><p>トリム範囲のキャッシュの消去に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NO_RANGES_PROCESSED</strong></p></td>
<td align="left"><p>Trim 範囲配列内の範囲が処理されませんでした。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

特定の記憶装置でトリムを実行すると、将来の書き込みパフォーマンスが大幅に向上する可能性があります。 また、Trim では、仮想プロビジョニングされたストレージシステム内の割り当てプールにリソースが返されます。 仮想ディスク上のファイルが削除されても、仮想ディスクファイル自体のサイズは変更されません。 仮想ディスク上で解放されたデータ範囲は、仮想ディスクファイルが置かれている物理記憶域上では切り捨てられません。 仮想ディスクデバイスは、 **FSCTL\_ファイル\_レベル\_TRIM**要求を使用して、仮想ディスクファイル内の特定のデータ範囲を物理記憶装置でトリミングできることをファイルシステムに通知することができます。 次に、ファイルシステムは、物理記憶域にトリム要求を発行します。 **FSCTL\_FILE\_LEVEL\_TRIM**要求は、データベースまたはメモリスワップファイルを管理するサービスアプリケーションによって発行されることもあります。

**FSCTL\_file\_LEVEL\_trim**コントロールコードは、ファイルの選択されたバイト範囲を記憶装置からトリミングしようとします。 バイト範囲は、[**ファイル\_レベル\_TRIM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)構造体の**範囲**配列に含まれています。 **範囲**の配列に含まれているのは、 [ **\_範囲構造\_トリム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_range)する1つ以上のファイル\_レベルです。

範囲配列に重複する範囲を含めることは、必ずしもエラー条件であるとは限りません。 これは、基になるストレージでエクステント処理がどのように処理されるかによって異なります。

切り捨てられた範囲は、ファイルシステムキャッシュからページとして削除されます。 キャッシュページのサイズと一致させるために、トリミング範囲の長さは**ページ\_サイズ**の倍数に調整されます。 また、トリミング範囲のオフセットがページの境界から始まらない場合は、次のページの境界に合わせて調整されます。 これらの制約を使用すると、オフセットがページに合わせられていない場合、または長さがページサイズが複数でない場合に、トリム範囲の長さが減少します。 元の長さが2ページ未満でオフセットがページに合わせられていない場合、トリム範囲の長さは0に短縮される可能性があります。

Trim 範囲が指定されている場合、またはファイルの終わり (EOF) を超えてページが調整された場合、範囲は無視されます。 ただし、EOF より前に配置され、長さが EOF を超える範囲オフセットは、ページサイズが複数 &lt;= EOF に調整されます。

圧縮または暗号化されたファイル (**属性\_フラグ\_圧縮\_マスク**または**属性\_フラグ\_暗号化さ**れた属性が設定されているファイル) では、ファイルレベルのトリミングはサポートされていません。

ファイルのトリミングは、トランザクションの外部で実行されます。 トリム操作をロールバックできません。

スパースファイル (**属性\_\_フラグ**が設定されているファイル) を使用すると、ファイルの未割り当て部分のトリム範囲は無視されます。

出力*バッファー*に含まれている場合、 **numrangesprocessed**された[**ファイル\_レベル\_trim\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_output)は、正常に処理されたトリミング範囲の数を示します。 Trim 範囲の処理中にエラーが発生した場合、 **Numrangesprocessed**は、残りの未処理の範囲の開始インデックスを指定します。これは、[**ファイル\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)の**numof**メンバーで終わり\_trim-1 です。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_レベル\_TRIM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim)

[**ファイル\_レベル\_TRIM\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_output)

[**ファイル\_レベル\_TRIM\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_level_trim_range)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






