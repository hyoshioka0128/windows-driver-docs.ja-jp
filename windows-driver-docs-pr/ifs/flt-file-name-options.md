---
title: FLT_FILE_NAME_OPTIONS
description: FLT\_ファイル\_名前\_オプション
ms.assetid: 6e21c11e-d2c8-4c57-8225-1fbc365cbbac
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cffba2edcd9116c1ebe12c1e5096276d92e76973
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350277"
---
# <a name="fltfilenameoptions"></a>FLT\_ファイル\_名前\_オプション





FLT\_ファイル\_名前\_オプションの種類は名の形式、クエリ メソッドをおよびファイル名の情報のクエリのフラグを指定するフラグのビットマスクを指定します。

```cpp
typedef ULONG FLT_FILE_NAME_OPTIONS; 
#define FLT_VALID_FILE_NAME_FORMATS 0x000000ff
    #define FLT_FILE_NAME_NORMALIZED    0x01
    #define FLT_FILE_NAME_OPENED        0x02
    #define FLT_FILE_NAME_SHORT         0x03
#define FLT_VALID_FILE_NAME_QUERY_METHODS 0x0000ff00
    #define FLT_FILE_NAME_QUERY_DEFAULT     0x0100
    #define FLT_FILE_NAME_QUERY_CACHE_ONLY  0x0200
    #define FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY 0x0300
    #define FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP 0x0400
#define FLT_VALID_FILE_NAME_FLAGS 0xff000000
    #define FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER 0x01000000
    #define FLT_FILE_NAME_DO_NOT_CACHE                  0x02000000
```

ビット 0 ~ 7 を使用してクエリできるファイル形式を示すため、 [ **FltGetFileNameFormat** ](https://msdn.microsoft.com/library/windows/hardware/ff543030)マクロ。 これらの形式の詳細については、次を参照してください。 [ **FLT\_ファイル\_名前\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544633)します。 現在、次の値が定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_NORMALIZED</p></td>
<td align="left"><p>正規化されたファイルの名前。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_OPENED</p></td>
<td align="left"><p>このファイルへのハンドルが開かれたときに使用された名前です。 この名前は正規化されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_SHORT</p></td>
<td align="left"><p>ファイルの短い形式 (8.3) の名前。 ファイルの短い名前は、ボリューム名、ディレクトリのパス、またはストリーム名には含まれません。 この名前は正規化されていません。</p></td>
</tr>
</tbody>
</table>

 

8 ~ 15 のビットを使用してクエリできるフィルター マネージャーによって使用されるファイル名のクエリ メソッドを指定する、 [ **FltGetFileNameQueryMethod** ](https://msdn.microsoft.com/library/windows/hardware/ff543040)マクロ。 これらの値の詳細については、次を参照してください。 [ **FltGetFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543032)します。 現在、次の値が定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_QUERY_DEFAULT</p></td>
<td align="left"><p>場合は、ファイル名のファイル システムのクエリを現在安全ではありません、何もありません。 それ以外の場合、ファイル名の情報のフィルター マネージャーの名前のキャッシュをクエリします。 キャッシュで名前が見つからない場合は、ファイル システムのクエリ実行し、結果をキャッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_QUERY_CACHE_ONLY</p></td>
<td align="left"><p>フィルター マネージャーの名前のキャッシュ ファイル名の情報のクエリを実行します。 ファイル システムをクエリできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_QUERY_FILESYSTEM_ONLY</p></td>
<td align="left"><p>ファイル名については、ファイル システムのクエリを実行します。 フィルター マネージャーの名前のキャッシュを照会できませんし、ファイル システムのクエリの結果をキャッシュしません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_QUERY_ALWAYS_ALLOW_CACHE_LOOKUP</p></td>
<td align="left"><p>フィルター マネージャーの名前のキャッシュ ファイル名の情報のクエリを実行します。 場合は、キャッシュで名前が見つからないし、現在、これを行うには安全では、ファイル名については、ファイル システム クエリを実行し、結果をキャッシュします。</p></td>
</tr>
</tbody>
</table>

 

16 ~ 23 のビットは、現在使用されていません。

24 ~ 31 のビットは、ファイル名のフラグを指定する名前のプロバイダー ミニフィルターによって使用されます。 現在、次の値が定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_REQUEST_FROM_CURRENT_PROVIDER</p></td>
<td align="left"><p>名前のプロバイダー ミニフィルター自体 (プロバイダー名のミニフィルター) に、スタック内の下位の名前のプロバイダーによって満たされたのではなく、名前のクエリ要求がリダイレクトされるかを指定するのにこのフラグを使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLT_FILE_NAME_DO_NOT_CACHE</p></td>
<td align="left"><p>このフラグは、このクエリから取得した名前をキャッシュしないことを示します。 プロバイダー ミニフィルターの名前は、名前を生成する中間のクエリを実行したときに、このフラグを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLT_FILE_NAME_ALLOW_QUERY_ON_REPARSE</p></td>
<td align="left"><p>名前のプロバイダー ミニフィルターは、このフラグを使用してクエリ内の名前にも安全であるかを指定することができます、status_reparse を不確実が返された場合でも、後のパスを作成します。 呼び出し元のことを確認する必要があります、 <strong>FileObject -&gt;FileName</strong>フィールドは変更されませんでした。 マウント ポイントやシンボリック リンクの再解析ポイントでこのフラグを使わないでください。</p>
<p>このフラグは、Microsoft Windows Server 2003 SP1 で使用可能な以降です。 このフラグも Windows 2000 SP4 の更新プログラムのロールアップ 1 以降で使用できます。</p></td>
</tr>
</tbody>
</table>

 

要件: fltkernel.h (fltkernel.h を含む)

## <a name="related-topics"></a>関連トピック


[**FLT\_FILE\_NAME\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff544633)

[**FltGetDestinationFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543003)

[**FltGetFileNameFormat**](https://msdn.microsoft.com/library/windows/hardware/ff543030)

[**FltGetFileNameInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543032)

[**FltGetFileNameInformationUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff543035)

[**FltGetFileNameQueryMethod**](https://msdn.microsoft.com/library/windows/hardware/ff543040)

 

 






