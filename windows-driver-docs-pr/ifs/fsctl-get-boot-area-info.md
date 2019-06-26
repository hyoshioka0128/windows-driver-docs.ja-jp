---
title: FSCTL_GET_BOOT_AREA_INFO 制御コード
description: FSCTL\_取得\_ブート\_領域\_情報制御コードは、ボリュームのブート セクターの場所を取得します。
ms.assetid: 0e842609-65f9-4a61-ab7f-f525650dfd14
keywords:
- FSCTL_GET_BOOT_AREA_INFO 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 65a58b4a2a751609de947995ad3996d84ed73eee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365040"
---
# <a name="fsctlgetbootareainfo-control-code"></a>FSCTL\_取得\_ブート\_領域\_情報制御コード


**FSCTL\_取得\_ブート\_領域\_情報**制御コードは、ボリュームのブート セクターの場所を取得します。

この操作を実行するには、呼び出し、 [ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)関数または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)を次の関数パラメーター。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 対象のボリュームのファイル オブジェクト ポインター **FSCTL\_取得\_ブート\_領域\_情報**ブート情報が取得されます。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 対象のボリュームのファイル ハンドル**FSCTL\_取得\_ブート\_領域\_情報**ブート情報が取得されます。 このパラメーターが必要とすることはできません**NULL**します。

Se、このハンドルを開く必要がある\_管理\_ボリューム\_アクセス権の名前。 詳細については、次を参照してください。[ファイルのセキュリティとアクセス権](https://docs.microsoft.com/windows/desktop/FileIO/file-security-and-access-rights)します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 使用**FSCTL\_取得\_ブート\_領域\_情報**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作で使用できません。 設定**NULL**します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作で使用できません。 0 に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
ポインターを[**ブート\_領域\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_boot_area_info)構造体は、ボリュームのブート セクターの場所を受信します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
(バイト単位)、出力バッファーのサイズ。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)など、次のいずれかの適切な NTSTATUS 値を返します。

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
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>操作が正常に完了しました。 OutputBuffer にはへのポインターが含まれています、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_boot_area_info" data-raw-source="[&lt;strong&gt;BOOT_AREA_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_boot_area_info)"> <strong>BOOT_AREA_INFO</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>パラメーターが無効です。たとえば、使用されるハンドルは、有効なボリュームのハンドルではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>OutputBuffer が結果十分な大きさではありません。 バッファーに情報が書き込まれたありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>ユーザーには、SE_MANAGE_VOLUME アクセスはありません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**FSCTL\_取得\_ブート\_領域\_情報**制御コードは、FastFAT および exFAT のデバイスで使用できます。 この機能は、フラッシュ ドライブなどのデバイス用の BitLocker の使用をサポートします。

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
<td align="left"><p>Windows Server 2008 R2、Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

 

 






