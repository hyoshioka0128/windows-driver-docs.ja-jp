---
title: FLT_PARAMETERS IRP_MJ_DEVICE_CONTROL と IRP_MJ_INTERNAL_DEVICE_CONTROL 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_デバイス\_コントロールまたは IRP\_MJ\_内部\_デバイス\_コントロール。
ms.assetid: ed2da1d5-838e-41a4-9a26-c61518da9cf3
keywords:
- FLT_PARAMETERS IRP_MJ_DEVICE_CONTROL と IRP_MJ_INTERNAL_DEVICE_CONTROL 共用体インストール可能なファイル システム ドライバー
- FLT_PARAMETERS union インストール可能なファイル システム ドライバー
- PFLT_PARAMETERS 共用体ポインター インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 5968caf46cf9f62b4f79c3792022716b8d9707f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580723"
---
# <a name="fltparameters-for-irpmjdevicecontrol-and-irpmjinternaldevicecontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_デバイス\_コントロールと IRP\_MJ\_内部\_デバイス\_コントロール共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
    } Common;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Neither;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   SystemBuffer;
    } Buffered;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputSystemBuffer;
      PVOID                   OutputBuffer;
      PMDL                    OutputMdlAddress;
    } Direct;
    struct {
      ULONG                   OutputBufferLength;
      ULONG POINTER_ALIGNMENT InputBufferLength;
      ULONG POINTER_ALIGNMENT IoControlCode;
      PVOID                   InputBuffer;
      PVOID                   OutputBuffer;
    } FastIo;
  } DeviceIoControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**DeviceIoControl**  
**一般的です**  
バッファリングのすべてのメソッドで使用されるコンポーネントの共用体。

**OutputBufferLength**  
バッファーのバイト単位の長さを**Neither.OutputBuffer**、 **Direct.OutputBuffer**、または**FastIo.OutputBuffer**へのポインターします。

**InputBufferLength**  
バッファーのバイト単位の長さを**Neither.InputBuffer**、 **Buffered.SystemBuffer**、 **Direct.InputSystemBuffer**、または**FastIo.InputBuffer**へのポインターします。

**IoControlCode**  
ターゲット デバイスのデバイス ドライバーに渡される IOCTL 関数コードです。

IOCTL 要求の詳細については、次を参照してください[I/O 制御コードを使用して](https://msdn.microsoft.com/library/windows/hardware/ff565406)で、*カーネル モードのアーキテクチャ ガイド*と"デバイスの入力と出力の制御コード"、Microsoft Windows sdk。ドキュメントです。 (このリソースできない場合がありますのいくつかの言語および国。)

**どちらも**  
共用体のコンポーネントがバッファー メソッドがメソッドである場合に使用\_NEITHER します。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://msdn.microsoft.com/library/windows/hardware/ff543023)で、*カーネル モードのアーキテクチャ ガイド*します。

**InputBuffer**  
操作の元の要求者が提供される入力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)、 [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)と[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](https://msdn.microsoft.com/library/windows/hardware/ff565432)と[ユーザー スペースのアドレスを参照するエラー](https://msdn.microsoft.com/library/windows/hardware/ff544308)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)、 [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)と[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](https://msdn.microsoft.com/library/windows/hardware/ff565432)と[ユーザー スペースのアドレスを参照するエラー](https://msdn.microsoft.com/library/windows/hardware/ff544308)で、*カーネル モードのアーキテクチャ ガイド*します。

**OutputMdlAddress**  
バッファーを記述したメモリ記述子一覧 (MDL) のアドレスを*Neither.OutputBuffer*へのポインターします。 このメンバーは省略可能とは、 **NULL**します。

**バッファー**  
共用体のコンポーネントがバッファー メソッドがメソッドである場合に使用\_バッファーに格納されました。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://msdn.microsoft.com/library/windows/hardware/ff543023)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**SystemBuffer**  
操作のシステムによって割り当てられたバッファーのアドレス。 メソッドで\_バッファー I/O、このバッファーが使用されるの入力し、出力の両方。 詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://msdn.microsoft.com/library/windows/hardware/ff554436)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**ダイレクト**  
共用体のコンポーネントがバッファー メソッドがメソッドである場合に使用\_IN\_ダイレクトまたはメソッド\_アウト\_ダイレクトします。 バッファリング メソッドの詳細については、次を参照してください。 [I/O 制御コードを定義する](https://msdn.microsoft.com/library/windows/hardware/ff543023)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**InputSystemBuffer**  
操作の入力バッファーのアドレス。 このバッファーに安全にカーネル モードからアクセスできるように、オペレーティング システムによってダウン ロックされています。 詳細については、次を参照してください。[メソッドにアクセスするデータ バッファーの](https://msdn.microsoft.com/library/windows/hardware/ff554436)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 メソッドとは異なり、直接 i/o\_I/O のどちらも、オペレーティング システムがロック ダウンこのバッファーはカーネル モードからにアクセスする安全なミニフィルターが I/O 操作の元の要求者と同じプロセス コンテキストである限りようにします。 (それ以外の場合に呼び出す必要があります[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)にメモリの記述子のリスト (MDL) からシステムのアドレスを取得、 **OutputMdlAddress**へのポインター.)詳細については、次を参照してください。[を使用して直接 I/O](https://msdn.microsoft.com/library/windows/hardware/ff565372)と[ダイレクト I/O エラー](https://msdn.microsoft.com/library/windows/hardware/ff544300)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputMdlAddress**  
MDL バッファーを記述するアドレスを**Direct.OutputBuffer**へのポインターします。 このメンバーが必要とすることはできません**NULL**します。

**FastIo**  
共用体のコンポーネントで使用されるときに、 [ **FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)構造が高速な I/O IRP を表す\_MJ\_デバイス\_コントロール操作です。

**InputBuffer**  
操作の元の要求者が提供される入力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)、 [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)と[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[ユーザー スペースのアドレスを参照するエラー](https://msdn.microsoft.com/library/windows/hardware/ff544308)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

**OutputBuffer**  
操作の元の要求者が指定された出力バッファーのユーザー モード仮想アドレス。 I/O マネージャーとフィルター マネージャーでは、これらのアドレスは検証されません。 ユーザー領域のアドレスは有効なは、ミニフィルターなどでルーチンを使用する必要があります、 [ **ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)、 [ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)と[ **FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)、内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。 詳細については、次を参照してください。[ユーザー スペースのアドレスを参照するエラー](https://msdn.microsoft.com/library/windows/hardware/ff544308)で、*カーネル モードのアーキテクチャ ガイド*します。 (このリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の構造体[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)操作には、IRP ベースのパラメーターが含まれています。コールバック データによって表されるデバイス-I/O-制御情報操作 ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)構造体。

IRP\_MJ\_デバイス\_IRP ベース操作または I/O 操作が高速コントロールであることができます。

IRP\_MJ\_内部\_デバイス\_コントロールは IRP ベースの I/O 操作です。

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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542046)

[**FltLockUserBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff543371)

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)

[**IRP\_MJ\_DEVICE\_CONTROL**](irp-mj-device-control.md)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)

[**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)

[**MmProbeAndLockPages**](https://msdn.microsoft.com/library/windows/hardware/ff554664)

[**ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)

[**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






