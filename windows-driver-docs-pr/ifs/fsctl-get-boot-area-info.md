---
title: FSCTL_GET_BOOT_AREA_INFO 制御コード
description: FSCTL\_GET\_BOOT\_AREA\_INFO 制御コードは、ボリュームのブートセクターの場所を取得します。
ms.assetid: 0e842609-65f9-4a61-ab7f-f525650dfd14
keywords:
- FSCTL_GET_BOOT_AREA_INFO 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_GET_BOOT_AREA_INFO
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb2be7ba2e923b6c8f09ada2c44b8fa1bbd0e5c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841312"
---
# <a name="fsctl_get_boot_area_info-control-code"></a>FSCTL\_\_ブート\_領域\_情報制御コードを取得する


**FSCTL\_GET\_boot\_AREA\_INFO**制御コードは、ボリュームのブートセクターの場所を取得します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)関数または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)関数を呼び出します。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ブート情報を取得する**FSCTL\_GET\_boot\_\_領域**のボリュームのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ブート情報を取得する、 **FSCTL\_GET\_ブート\_\_領域**のボリュームのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

\_ボリューム\_名前のアクセス権を管理\_には、このハンドルを SE で開く必要があります。 詳細については、「[ファイルセキュリティとアクセス権](https://docs.microsoft.com/windows/desktop/FileIO/file-security-and-access-rights)」を参照してください。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作については、FSCTL\_使用して **\_ブート\_領域\_情報を取得**してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。 を**NULL**に設定します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。 を0に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
ボリュームのブートセクターの場所を受け取る、[**ブート\_領域\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_boot_area_info)構造体へのポインター。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
出力バッファーのサイズ (バイト単位)。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、次のいずれかのような適切な NTSTATUS 値を返します。

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
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>操作は成功しました。 OutputBuffer には、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_boot_area_info" data-raw-source="[&lt;strong&gt;BOOT_AREA_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_boot_area_info)"><strong>BOOT_AREA_INFO</strong></a>構造体へのポインターが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>パラメーターが有効ではありませんでした。たとえば、使用されるハンドルが有効なボリュームハンドルではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer は、結果に対して十分な大きさではありません。 バッファーに情報が書き込まれていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>ユーザーには、SE_MANAGE_VOLUME アクセス権がありません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**FSCTL\_\_ブート\_領域の取得\_情報**制御コードは、FastFAT および exFAT デバイスで使用できます。 この機能は、フラッシュドライブなどのデバイスでの BitLocker の使用をサポートしています。

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
<td align="left"><p>Windows Server 2008 R2、Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

 

 






