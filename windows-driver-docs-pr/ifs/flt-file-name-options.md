---
title: FLT_FILE_NAME_OPTIONS
description: FLT\_ファイル\_名前\_オプション
ms.assetid: 6e21c11e-d2c8-4c57-8225-1fbc365cbbac
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dabc22438898e36c8cd546280874b5f460ddb4bb
ms.sourcegitcommit: 95e3fd15d9c00a341e774d58a927856d750a35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410017"
---
# <a name="fltfilenameoptions"></a>FLT\_ファイル\_名前\_オプション

FLT_FILE_NAME_OPTIONS 型は、名の形式、クエリ メソッドをおよびファイル名の情報のクエリのフラグを指定するフラグのビットマスクです。

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

ビット 0 ~ 7 を使用してクエリできるファイル形式を示すため、 [ **FltGetFileNameFormat** ](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))マクロ。 これらの形式の詳細については、次を参照してください。 [ **FLT_FILE_NAME_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_file_name_information)します。 現在、次の値が定義されています。

| 値 | 説明 |
| ----- | ------- |
| FLT_FILE_NAME_NORMALIZED | 正規化されたファイルの名前。 |
| FLT_FILE_NAME_OPENED | このファイルへのハンドルが開かれたときに使用された名前です。 この名前は正規化されていません。 |
| FLT_FILE_NAME_SHORT | ファイルの短い形式 (8.3) の名前。 ファイルの短い名前は、ボリューム名、ディレクトリのパス、またはストリーム名には含まれません。 この名前は正規化されていません。 |

8 ~ 15 のビットを使用してクエリできるフィルター マネージャーによって使用されるファイル名のクエリ メソッドを指定する、 [ **FltGetFileNameQueryMethod** ](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))マクロ。 これらの値の詳細については、次を参照してください。 [ **FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformation)します。 現在、次の値が定義されています。

| 値 | 説明 |
| ----- | ------- |
| FLT_FILE_NAME_QUERY_DEFAULT | 場合は、ファイル名のファイル システムのクエリを現在安全ではありません、何もありません。 それ以外の場合、ファイル名の情報のフィルター マネージャーの名前のキャッシュをクエリします。 キャッシュで名前が見つからない場合は、ファイル システムのクエリ実行し、結果をキャッシュします。 |
| FLT_FILE_NAME_QUERY_CACHE_ONLY | フィルター マネージャーの名前のキャッシュ ファイル名の情報のクエリを実行します。 ファイル システムをクエリできません。 |
| FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY | ファイル名については、ファイル システムのクエリを実行します。 フィルター マネージャーの名前のキャッシュを照会できませんし、ファイル システムのクエリの結果をキャッシュしません。 |
| FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP | フィルター マネージャーの名前のキャッシュ ファイル名の情報のクエリを実行します。 場合は、キャッシュで名前が見つからないし、現在、これを行うには安全では、ファイル名については、ファイル システム クエリを実行し、結果をキャッシュします。 |

16 ~ 23 のビットは、現在使用されていません。

24 ~ 31 のビットは、ファイル名のフラグを指定する名前のプロバイダー ミニフィルターによって使用されます。 現在、次の値が定義されています。

| 値 | 説明 |
| ----- | ------- |
| FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER | 名前のプロバイダー ミニフィルター自体 (プロバイダー名のミニフィルター) に、スタック内の下位の名前のプロバイダーによって満たされたのではなく、名前のクエリ要求がリダイレクトされるかを指定するのにこのフラグを使用できます。 |
| FLT_FILE_NAME_DO_NOT_CACHE | このフラグは、このクエリから取得した名前をキャッシュしないことを示します。 プロバイダー ミニフィルターの名前は、名前を生成する中間のクエリを実行したときに、このフラグを使用します。 |
| FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE | 名前のプロバイダー ミニフィルターは、このフラグを使用してクエリ内の名前にも安全であるかを指定することができます、status_reparse を不確実が返された場合でも、後のパスを作成します。 呼び出し元のことを確認する必要があります、 **FileObject ファイル名]-> [** フィールドは変更されませんでした。 マウント ポイントやシンボリック リンクの再解析ポイントでこのフラグを使わないでください。 |

## <a name="requirements"></a>要件

|   |   |
| - | - |
| **ヘッダー** | fltkernel.h (fltkernel.h を含む) |

## <a name="related-topics"></a>関連トピック

[**FLT_FILE_NAME_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_file_name_information)

[**FltGetDestinationFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetdestinationfilenameinformation)

[**FltGetFileNameFormat**](https://docs.microsoft.com/previous-versions/ff543030(v=vs.85))

[**FltGetFileNameInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformation)

[**FltGetFileNameInformationUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilenameinformationunsafe)

[**FltGetFileNameQueryMethod**](https://docs.microsoft.com/previous-versions/ff543040(v=vs.85))
