---
title: IRP_MJ_FILE_SYSTEM_CONTROL 共用体の FLT_PARAMETERS
description: FLT\_IO\_パラメーターの MajorFunction フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネント\_は、MJ\_ファイル\_システム\_コントロールです。
ms.assetid: d90b9f23-9fae-46e8-b68c-1ba11b3fa17a
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
- FLT_PARAMETERS union にインストール可能なファイルシステムドライバー
- PFLT_PARAMETERS union ポインターのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45c677b8b3f6899f54b3258b808681f6ac69a64f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841394"
---
# <a name="flt_parameters-for-irp_mj_file_system_control-union"></a>IRP\_MJ\_ファイル\_システム\_コントロール共用体の FLT\_パラメーター


[**FLT\_IO\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)の**MajorFunction**フィールドが操作の\_ブロック構造体である場合に使用される共用体コンポーネント\_は、 [**MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      PVPB           Vpb;
      PDEVICE_OBJECT DeviceObject;
    } VerifyVolume;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
    } Common;
    struct {
      ULONG                    OutputBufferLength;
      ULONG POINTER_ALIGNMENT  InputBufferLength;
      ULONG POINTER_ALIGNMENT  FsControlCode;
      PVOID                    InputBuffer;
      PVOID                    OutputBuffer;
      PMDL                     OutputMdlAddress;
    } Neither;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
      PVOID                   SystemBuffer;
    } Buffered;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT FsControlCode;
      PVOID                   InputSystemBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Direct;
  } FileSystemControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**FileSystemControl**  
次のメンバーを含む構造体。

**VerifyVolume**  
IRP\_に使用される共用体コンポーネント。\_ボリューム操作を確認\_ます。

**Vpb**  
検証するボリュームのボリュームパラメーターブロック (VPB) へのポインター。

**DeviceObject**  
検証するボリュームのデバイスオブジェクトへのポインター。

**的**  
IRP\_すべてのバッファリングメソッドに使用される共用体コンポーネント\_カーネル\_呼び出しおよび IRP\_、ユーザー\_FS\_要求操作を実行します。

**OutputBufferLength**  
**Outputbuffer**または**Direct**によって参照されていないバッファーの長さ (バイト単位)。

**InputBufferLength**  
**InputBuffer**、**バッファリングされた systembuffer**、または**直接の inputsystembuffer**メンバーが指すバッファーの長さ (バイト単位)。

**FsControlCode**  
ターゲットデバイスのファイルシステム、ファイルシステムフィルター、またはミニフィルタードライバーに渡される FSCTL 関数コード。

IOCTL 要求と FSCTL 要求の詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」および Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**両者**  
IRP\_に使用される共用体コンポーネント\_カーネル\_呼び出しおよび IRP\_、ユーザー\_FS\_要求操作 (バッファリングメソッドがメソッドである場合\_) ではありません。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**InputBuffer**  
操作の元の要求元が指定した入力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[バッファーを使用し](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)た[ユーザー領域のアドレスの参照](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**  
操作の元の要求元が指定した出力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[バッファーを使用し](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)た[ユーザー領域のアドレスの参照](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputMdlAddress**  
**Outputbuffer**メンバーが指しているバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

**付き**  
IRP\_に使用される共用体コンポーネント\_カーネル\_呼び出しおよび IRP\_、ユーザー\_FS\_要求操作 (バッファリングメソッドがメソッド\_がバッファリングされている場合)。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**SystemBuffer**  
操作に対してシステムが割り当てたバッファーのアドレス。 メソッド\_バッファー i/o では、このバッファーは入力と出力の両方に使用されます。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**接続**  
IRP\_に使用される共用体コンポーネント\_カーネル\_呼び出しと IRP\_は、\_DIRECT または METHOD でのバッファリングメソッドがメソッド\_の場合、ユーザー\_FS\_要求操作\_OUT\_DIRECT。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。

**InputSystemBuffer**  
操作の入力バッファーのアドレス。 このバッファーは、カーネルモードから安全にアクセスできるように、オペレーティングシステムによってロックされています。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**  
操作の元の要求元が指定した出力バッファーのユーザーモード仮想アドレス。 ダイレクト i/o では、i/o 操作の元の要求元と同じプロセスコンテキストでミニフィルターが使用されている限り、オペレーティングシステムは i/o ではない\_方法で、このバッファーをロックダウンして、カーネルモードから安全にアクセスできるようにします。 (それ以外の場合は、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出して、 **Outputmdladdress**メンバーが指す MDL からシステムアドレスを取得する必要があります)。詳細については、「*カーネルモードアーキテクチャガイド*」の「direct I/o と[エラーをダイレクト I/o で](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)[使用する](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputMdlAddress**  
**直接の outputbuffer**メンバーが指すバッファーを記述する MDL のアドレス。 このメンバーは必須であり、 **NULL**にすることはできません。

<a name="remarks"></a>注釈
-------

[**IRP\_MJ\_ファイル\_システム\_制御**](irp-mj-file-system-control.md)操作の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータによって表されるファイルシステム制御情報操作のパラメーターが含まれています ([**FLT @noデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)構造の\_) 構造体。 これは、 [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

IRP\_MJ\_ファイル\_システム\_制御は、IRP ベースの操作です。

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
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoVerifyVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioverifyvolume)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






