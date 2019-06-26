---
title: FSCTL_SET_ZERO_DATA 制御コード
description: FSCTL\_設定\_0\_データ制御コードがゼロ (0) を使用するファイルの指定した範囲を入力します。
ms.assetid: AEC4DAD4-17EB-412B-881B-E54F6A578637
keywords:
- FSCTL_SET_ZERO_DATA 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_ZERO_DATA
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ddcebb0ad5041c287882cd92fbefa332f2c8088
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366224"
---
# <a name="fsctlsetzerodata-control-code"></a>FSCTL\_設定\_0\_データ制御コード


**FSCTL\_設定\_0\_データ**制御コードがゼロ (0) を使用するファイルの指定した範囲を入力します。 ファイルはスパースまたは圧縮された場合、NTFS ファイル システムはファイル内のディスク領域を解放できます。 これには、ゼロ (0)、ファイルのサイズを拡張せずにバイトの範囲を設定します。

ドライバーからこの操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance"></a>*インスタンス*  
呼び出し元のポインターを不透明なインスタンス。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fileobject"></a>*FileObject*  
値にゼロを書き込むファイルへのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。

使用**FSCTL\_設定\_0\_データ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
ポインターを[**ファイル\_0\_データ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information)または[**ファイル\_0\_データ\_情報\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information_ex)をゼロに設定するファイルの範囲を指定します。

**FileOffset**メンバーがゼロ (0) に設定する最初のバイトのバイト オフセットと**BeyondFinalZero**メンバーは、バイトの最後の最初のバイトのゼロ (0) のバイト オフセットします。

**フラグ**メンバー [**ファイル\_0\_データ\_情報\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information_ex)に修飾子を指定します、操作です。 たとえば、**フラグ**に設定されている**ファイル\_0\_データ\_情報\_フラグ\_保持\_CACHED\_データ**、このファイルの範囲に対応するキャッシュの内容を削除できません。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
(バイト単位)、入力バッファーのサイズ。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)返します**状態\_成功**NTSTATUS は、適切な値。

-   **ステータス\_不十分\_リソース**が、操作を完了するのに十分なメモリがない場合に返されます。
-   **ステータス\_無効な\_パラメーター**ときに返される、 *InputBufferLength*のサイズよりも小さい、**ファイル\_0\_データ\_情報**構造体または指定されたファイルがシステム メタデータ ファイルまたはディレクトリ。
-   **ステータス\_アクセス\_DENIED**ときに返される、**ファイル\_0\_データ\_情報\_フラグ\_保持\_キャッシュされた\_データ**ユーザー モードから設定されます。
-   **ステータス\_メディア\_書き込み\_PROTECTED**かどうか、ボリュームは現在書き込み禁止が返されます。

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

[**ファイル\_0\_データ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information)

[**ファイル\_0\_データ\_情報\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_zero_data_information_ex)

 

 






