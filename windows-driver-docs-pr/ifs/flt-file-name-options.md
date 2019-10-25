---
title: FLT_FILE_NAME_OPTIONS
description: FLT\_ファイル\_名\_オプション
ms.assetid: 6e21c11e-d2c8-4c57-8225-1fbc365cbbac
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e8e292eb47c73a85871c05a21b0d0141c40c361
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841392"
---
# <a name="flt_file_name_options"></a>FLT\_ファイル\_名\_オプション

FLT_FILE_NAME_OPTIONS 型は、ファイル名情報クエリの名前の形式、クエリメソッド、およびフラグを指定するフラグのビットマスクです。

```cpp
typedef ULONG FLT_FILE_NAME_OPTIONS;
#define FLT_VALID_FILE_NAME_FORMATS                       0x000000ff
    #define FLT_FILE_NAME_NORMALIZED                      0x00000001
    #define FLT_FILE_NAME_OPENED                          0x00000002
    #define FLT_FILE_NAME_SHORT                           0x00000003
#define FLT_VALID_FILE_NAME_QUERY_METHODS                 0x0000ff00
    #define FLT_FILE_NAME_QUERY_DEFAULT                   0x00000100
    #define FLT_FILE_NAME_QUERY_CACHE_ONLY                0x00000200
    #define FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY           0x00000300
    #define FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP 0x00000400
#define FLT_VALID_FILE_NAME_FLAGS                         0xff000000
    #define FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER   0x01000000
    #define FLT_FILE_NAME_DO_NOT_CACHE                    0x02000000
    #define FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE          0x04000000
```

ビット 0 ~ 7 はファイル形式を示し、 [**FltGetFileNameFormat**](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))マクロを使用してクエリを実行できます。 これらの形式の詳細については、「 [**FLT_FILE_NAME_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_file_name_information)」を参照してください。 現在、次の値が定義されています。

| Value | 意味 |
| ----- | ------- |
| FLT_FILE_NAME_NORMALIZED | ファイルの正規化された名前。 |
| FLT_FILE_NAME_OPENED | ハンドルがこのファイルに開かれたときに使用された名前。 この名前は正規化されていません。 |
| FLT_FILE_NAME_SHORT | ファイルの短い (8.3) 名前。 ファイルの短い名前には、ボリューム名、ディレクトリパス、またはストリーム名は含まれません。 この名前は正規化されていません。 |

Bits 8 ~ 15 では、フィルターマネージャーによって使用されるファイル名のクエリ方法を指定します。このメソッドには、 [**FltGetFileNameQueryMethod**](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))マクロを使用してクエリを実行できます。 これらの値の詳細については、「 [**FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformation)」を参照してください。 現在、次の値が定義されています。

| Value | 意味 |
| ----- | ------- |
| FLT_FILE_NAME_QUERY_DEFAULT | ファイル名のファイルシステムに対してクエリを実行するのが現在安全でない場合は、何も行いません。 それ以外の場合は、フィルターマネージャーの名前キャッシュでファイル名情報を照会します。 名前がキャッシュに見つからない場合は、ファイルシステムに対してクエリを実行し、結果をキャッシュします。 |
| FLT_FILE_NAME_QUERY_CACHE_ONLY | フィルターマネージャーの名前キャッシュでファイル名情報を照会します。 ファイルシステムに対してクエリを実行しないでください。 |
| FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY | ファイルシステムでファイル名情報を照会します。 フィルターマネージャーの名前キャッシュに対してクエリを実行しないでください。また、ファイルシステムクエリの結果をキャッシュしません。 |
| FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP | フィルターマネージャーの名前キャッシュでファイル名情報を照会します。 名前がキャッシュ内に見つからず、その名前が現在安全である場合は、ファイルシステムに対してファイル名情報を照会し、結果をキャッシュします。 |

ビット 16 ~ 23 は現在使用されていません。

名前プロバイダーミニフィルターでは、ファイル名フラグを指定するためにビット 24 ~ 31 が使用されます。 現在、次の値が定義されています。

| Value | 意味 |
| ----- | ------- |
| FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER | 名前プロバイダーのミニフィルターでは、このフラグを使用して、名前のクエリ要求をスタック内の下位の名前プロバイダーによって満たされるのではなく、自身 (名前プロバイダーミニフィルター) にリダイレクトするように指定できます。 |
| FLT_FILE_NAME_DO_NOT_CACHE | このフラグは、このクエリから取得した名前がキャッシュされないことを示します。 Name provider ミニフィルターは、中間クエリを実行して名前を生成するときに、このフラグを使用します。 |
| FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE | 名前プロバイダーのミニパスでは、このフラグを使用して、STATUS_REPARSE が返された場合でも、作成後のパスで名前をクエリするのが安全であることを指定できます。 **FileObject > FileName**フィールドが変更されていないことを確認するのは、呼び出し元の責任です。 マウントポイントやシンボリックリンクの再解析ポイントでは、このフラグを使用しないでください。 |

## <a name="requirements"></a>要件

|   |   |
| - | - |
| **項目** | fltkernel .h (fltkernel. h を含む) |

## <a name="related-topics"></a>関連トピック

[**FLT_FILE_NAME_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_file_name_information)

[**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)

[**FltGetFileNameFormat**](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))

[**FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformation)

[**FltGetFileNameInformationUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilenameinformationunsafe)

[**FltGetFileNameQueryMethod**](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))
