---
title: IRP_MJ_FILE_SYSTEM_CONTROL 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_FILE_SYSTEM_CONTROL 場合に使用される共用体コンポーネント。
ms.assetid: d90b9f23-9fae-46e8-b68c-1ba11b3fa17a
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- PFLT_PARAMETERS 共用体ポインターのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 02/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 854cc1fe98305c2a961cb783086f1e34f73a4edd
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072243"
---
# <a name="flt_parameters-for-irp_mj_file_system_control-union"></a>IRP_MJ_FILE_SYSTEM_CONTROL 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_FILE_SYSTEM_CONTROL**](irp-mj-file-system-control.md)場合に使用される共用体コンポーネント。

## <a name="syntax"></a>構文

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

## <a name="members"></a>Members

**FileSystemControl**  
次のメンバーを含む構造体。

**VerifyVolume**  
IRP_MN_VERIFY_VOLUME 操作に使用される共用体コンポーネントです。

**Vpb**  
検証するボリュームのボリュームパラメーターブロック (VPB) へのポインター。

**DeviceObject**  
検証するボリュームのデバイスオブジェクトへのポインター。

**的**  
IRP_MN_KERNEL_CALL および IRP_MN_USER_FS_REQUEST 操作のすべてのバッファリングメソッドに使用される共用体コンポーネント。

**OutputBufferLength**  
**Outputbuffer**または**Direct**によって参照されていないバッファーの長さ (バイト単位)。

**InputBufferLength**  
**InputBuffer**、**バッファリングされた systembuffer**、または**直接の inputsystembuffer**メンバーが指すバッファーの長さ (バイト単位)。

**FsControlCode**  
ターゲットデバイスのファイルシステム、ファイルシステムフィルター、またはミニフィルタードライバーに渡される FSCTL 関数コード。

IOCTL 要求と FSCTL 要求の詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」および Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**両者**  
バッファリングメソッドが METHOD_NEITHER 場合に IRP_MN_KERNEL_CALL および IRP_MN_USER_FS_REQUEST 操作に使用される共用体コンポーネント。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**InputBuffer**  
操作の元の要求元が指定した入力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[バッファーを使用し](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)た[ユーザー領域のアドレスの参照](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**  
操作の元の要求元が指定した出力バッファーのユーザーモード仮想アドレス。 I/o マネージャーとフィルターマネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスが有効であることを確認するには、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)、 [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)などのルーチンを使用し**て、try/except**ブロック内のすべてのバッファー参照を含むようにする必要があります。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[バッファーを使用し](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-neither-buffered-nor-direct-i-o)た[ユーザー領域のアドレスの参照](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-referencing-user-space-addresses)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**は省略可能であり、MDL が指定されていない場合は NULL にすることができます。 **OutputMdlAddress**。 「**解説**」を参照してください。

**OutputMdlAddress**  
**Outputbuffer**メンバーが指しているバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、バッファーが**OutputBuffer のいずれにも**指定されていない場合は**NULL**にすることができます。

**付き**  
バッファリングメソッドが METHOD_BUFFERED 場合に IRP_MN_KERNEL_CALL および IRP_MN_USER_FS_REQUEST 操作に使用される共用体コンポーネント。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**SystemBuffer**  
操作に対してシステムが割り当てたバッファーのアドレス。 METHOD_BUFFERED i/o では、このバッファーは入力と出力の両方に使用されます。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**接続**  
バッファリングメソッドが METHOD_IN_DIRECT または METHOD_OUT_DIRECT 場合に、IRP_MN_KERNEL_CALL 操作および IRP_MN_USER_FS_REQUEST 操作に使用される共用体コンポーネント。 バッファリングメソッドの詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。

**InputSystemBuffer**  
操作の入力バッファーのアドレス。 このバッファーは、カーネルモードから安全にアクセスできるように、オペレーティングシステムによってロックされています。 詳細については、「*カーネルモードアーキテクチャガイド*」の「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputBuffer**  
操作の元の要求元が指定した出力バッファーのユーザーモード仮想アドレス。 ダイレクト i/o では、METHOD_NEITHER i/o とは異なり、オペレーティングシステムはこのバッファーをロックダウンして、ミニパスが i/o 操作の元の要求元と同じプロセスコンテキストにある限り、カーネルモードから安全にアクセスできるようにします。 (それ以外の場合は、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出して、 **Outputmdladdress**メンバーが指す MDL からシステムアドレスを取得する必要があります)。詳細については、「*カーネルモードアーキテクチャガイド*」の「direct I/o と[エラーをダイレクト I/o で](https://docs.microsoft.com/windows-hardware/drivers/kernel/errors-in-direct-i-o)[使用する](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o)」を参照してください。 (このリソースは、一部の言語および国では使用できません。)

**OutputMdlAddress**  
**直接の outputbuffer**メンバーが指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは必須であり、 **NULL**にすることはできません。

## <a name="remarks"></a>コメント

[**IRP_MJ_FILE_SYSTEM_CONTROL**](irp-mj-file-system-control.md)操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表されるファイルシステムコントロール情報操作のパラメーターが含まれています。 これは[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

**Outputbuffer**と**mdladdress**バッファーの両方が指定されていない場合は、ミニフィルターで MDL を使用することをお勧めします。

ミニフィルターによって、どちらの値**も**変更されない場合は、フィルターマネージャーによって、現在格納されている MDL のうち**mdladdress**が解放されます。 **mdladdress**の前の値は復元されません。

IRP_MJ_FILE_SYSTEM_CONTROL は、IRP ベースの操作です。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| ヘッダー | Fltkernel .h (Fltkernel. h を含む) |

## <a name="see-also"></a>参照

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoVerifyVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioverifyvolume)

[**IRP_MJ_FILE_SYSTEM_CONTROL**](irp-mj-file-system-control.md)

[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)

[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)
