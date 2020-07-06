---
title: IRP_MJ_QUERY_EA 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_QUERY_EA 場合に使用される共用体コンポーネント。
ms.assetid: 858e8c72-33ae-441c-ada9-86c5df0e4f59
keywords:
- IRP_MJ_QUERY_EA ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: a1ce7f523c91038efa1ebe855f010c13f1ff1c0b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967963"
---
# <a name="flt_parameters-for-irp_mj_query_ea-union"></a>IRP_MJ_QUERY_EA 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_QUERY_EA**](irp-mj-query-ea.md)場合に使用される共用体コンポーネント。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                    Length;
    PVOID                    EaList;
    ULONG                    EaListLength;
    ULONG  POINTER_ALIGNMENT EaIndex;
    PVOID                    EaBuffer;
    PMDL                     MdlAddress;
  } QueryEa;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>メンバー

**Quer**  
次のメンバーを含む FLT_PARAMETERS union 内の構造体。

**[データ型]**  
**EaBuffer**が指すバッファーの長さ (バイト単位)。

**EaList**  
クエリ対象の拡張属性を指定する、呼び出し元が指定した FILE_GET_EA_INFORMATION 構造化された入力バッファーへのポインター。

**EaListLength**  
**Ealist**が指すバッファーの長さ (バイト単位)。

**Eライド Dex**  
拡張属性リストのスキャンを開始する位置のエントリのインデックス。 操作の FLT_IO_PARAMETER_BLOCK 構造で SL_INDEX_SPECIFIED フラグが設定されていない場合、または**Ealist**が空でないリストを指している場合、このパラメーターは無視されます。

**EaBuffer**  
拡張属性値が返される、呼び出し元が指定した[**FILE_FULL_EA_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)構造の出力バッファーへのポインター。 このメンバーは省略可能であり、MDL が**Mdladdress**に指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

**MdlAddress**  
**EaBuffer**が指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **EaBuffer**でバッファーが指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

## <a name="remarks"></a>注釈

[**IRP_MJ_QUERY_EA**](irp-mj-query-ea.md)操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される、IRP ベースのクエリの拡張属性情報操作のパラメーターが含まれています。 これは FLT_IO_PARAMETER_BLOCK 構造体に含まれています。

**EaBuffer**と**mdladdress**の両方のバッファーを指定する場合は、ミニフィルターを使用することをお勧めします。 **EaBuffer**が指すメモリは、呼び出しプロセスのコンテキスト内でアクセスされているユーザーモードアドレスである場合、またはカーネルモードアドレスの場合に有効です。

ミニフィルターによって**mdladdress**の値が変更された場合、事後操作コールバックの後、フィルターマネージャーは現在**mdladdress**に格納されている MDL を解放し、 **mdladdress**の前の値を復元します。

IRP_MJ_QUERY_EA は、IRP ベースの操作です。

## <a name="requirements"></a>要件

**ヘッダー**: fltkernel .H (fltkernel .h を含む)


## <a name="see-also"></a>関連項目

[**FILE_FULL_EA_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckEaBufferValidity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IRP_MJ_QUERY_EA**](irp-mj-query-ea.md)
