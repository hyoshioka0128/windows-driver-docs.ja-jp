---
title: FSCTL_DISMOUNT_VOLUME 制御コード
description: FSCTL\_マウント解除\_ボリューム コントロールのコードはボリュームが使用されているかどうかに関係なく、ボリュームのマウントを解除しようとしています。
ms.assetid: edfff768-3bb3-4b8a-b982-80797ac116fd
keywords:
- FSCTL_DISMOUNT_VOLUME 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_DISMOUNT_VOLUME
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6112d6332da7043822789316854779b26a20bfb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365068"
---
# <a name="fsctldismountvolume-control-code"></a>FSCTL\_マウント解除\_ボリューム コントロール コード


**FSCTL\_マウント解除\_ボリューム**ボリュームが使用されているかどうかに関係なく、ボリュームのマウントを解除しようとコードを制御します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance"></a>*インスタンス*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 呼び出し元のポインターを不透明なインスタンス。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 マウントを解除するボリュームを指定する、ファイル ポインター オブジェクト。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 マウントを解除するボリュームのファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作のコードを制御します。 使用**FSCTL\_マウント解除\_ボリューム**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作で使用できません。 設定**NULL**します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
この操作で使用できません。 0 に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
この操作で使用できません。 設定**NULL**します。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength\[で\]*  
この操作で使用できません。 0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_成功または適切な NTSTATUS 値。

<a name="remarks"></a>コメント
-------

**FSCTL\_マウント解除\_ボリューム**制御コードは、他のプロセスに場合、それらのプロセスの予期しない結果を持つことができると、ボリュームを使用しているかどうかに関係なく、ボリュームのマウントを解除しようとします。ボリュームのロックを保持、操作を行います。 ボリュームのロックについては、次を参照してください。 [ **FSCTL\_ロック\_ボリューム**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_lock_volume)します。

オペレーティング システムでは、マウント ボリュームを検出しません。 マウントのボリュームにアクセスしようとすると、オペレーティング システムは、ボリュームのマウントを試みます。 呼び出しなど[ **GetLogicalDrives** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-getlogicaldrives)マウント ボリュームをマウントするオペレーティング システムをトリガーします。

*FileHandle*にハンドルが渡される[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)への直接アクセス用に開く、ボリュームを識別するハンドルである必要があります。 ボリュームのハンドルを取得する[ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)で、 *ObjectAttributes*パラメーターに設定する*ObjectName*次のフォーム:  *\\ \\.\\X:* 場所*X*はボリューム、フロッピー ディスク ドライブ、または CD-ROM ドライブのドライブ文字です。 アプリケーションでは、ファイルを指定する必要がありますも\_共有\_読み取りとファイル\_共有\_でフラグを書き込み、 *ShareAccess*パラメーターの**ZwCreateFile**.

指定されたボリュームでは、システム ボリュームまたはページのファイルが含まれています、操作が失敗します。

指定されたボリュームが別のプロセスによってロックされている場合、操作は失敗します。

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
<td align="left">Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






