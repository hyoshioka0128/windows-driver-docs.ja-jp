---
title: PropVariant ヘルパー
description: PropVariant のヘルパー関数は、センサーに関連付けられている PROPVARIANT 構造体を操作するため、v2 センサー ドライバーによって使用されます。
ms.assetid: 5A5A008A-399F-4464-ADD0-7F2DDACB6D4B
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb19c657d5e56b4459081b6645c3d48f4af60728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330071"
---
# <a name="propvariant-helpers"></a>PropVariant ヘルパー


PropVariant のヘルパー関数が操作に v2 センサー ドライバーによって使用される、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

ヘルパー関数は、センサー デバイス ドライバー ソフトウェア インターフェイス (DDSI) と共に使用されます。

**InitPropVariantFromFloat**

センサー DDSI による使用量

-   初期化します、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)構造体。

コメント

-   この関数は、浮動小数点数を受信し、次に、その変数に基づいて、作成して初期化する[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)構造体。

**PropKeyFindKeyGetPropVariant**

センサー DDSI による使用量

-   取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)構造体。

コメント

-   なし。

**PropKeyFindKeySetPropVariant**

センサー DDSI による使用量

-   セットを[PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)構造体。

コメント

-   なし。

**PropKeyFindKeyGetFileTime**

センサー DDSI による使用量

-   データ ファイルに関連付けられたタイムスタンプを取得します。

コメント

-   これは、 *filetime*のメンバー、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)指定したプロパティのキーに一致する構造体。

**PropKeyFindKeyGetGuid**

センサー DDSI による使用量

-   センサーの GUID を取得します。

コメント

-   これは、 *puuid*のメンバー、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)指定したプロパティのキーに一致する構造体。

**PropKeyFindKeyGetBool**

センサー DDSI による使用量

-   ブール値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropKeyFindKeyGetUlong**

センサー DDSI による使用量

-   ULONG 値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropKeyFindKeyGetUshort**

センサー DDSI による使用量

-   USHORT 値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropKeyFindKeyGetFloat**

センサー DDSI による使用量

-   浮動小数点値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropKeyFindKeyGetDouble**

センサー DDSI による使用量

-   DOUBLE 値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropKeyFindKeyGetInt32**

センサー DDSI による使用量

-   32 ビット値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropKeyFindKeyGetInt64**

センサー DDSI による使用量

-   64 ビット値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropKeyFindKeyGetNthUlong**

センサー DDSI による使用量

-   N 番目の ULONG 値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)内、指定したプロパティのキーに基づいているコレクションの一覧。

コメント

-   なし。

**PropKeyFindKeyGetNthUshort**

センサー DDSI による使用量

-   UShort の n 番目の値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)内、指定したプロパティのキーに基づいているコレクションの一覧。

コメント

-   なし。

**PropKeyFindKeyGetNthInt64**

センサー DDSI による使用量

-   N 番目の Int64 値を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)内、指定したプロパティのキーに基づいているコレクションの一覧。

コメント

-   なし。

**IsKeyPresentInPropertyList**

センサー DDSI による使用量

-   ブール値を返します。

コメント

-   ブール値でプロパティのキーが見つかったかどうかを示す、 [**センサー\_プロパティ\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)センサーに関連付けられている構造体。

**IsKeyPresentInCollectionList**

センサー DDSI による使用量

-   ブール値を返します。

コメント

-   ブール値でプロパティのキーが見つかったかどうかを示す、 [**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造体。 センサーに関連付けられています。

**IsCollectionListSame**

センサー DDSI による使用量

-   ブール値を返します。

コメント

-   2 つ[**センサー\_コレクション\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)を判断して、同じ構造体。

**PropVariantGetInformation**

センサー DDSI による使用量

-   について、サイズ、オフセット、およびその他の情報を取得、 [PROPVARIANT](https://docs.microsoft.com/windows/desktop/api/propidl/ns-propidl-tagpropvariant)センサーに関連付けられている構造体。

コメント

-   なし。

**PropertiesListCopy**

センサー DDSI による使用量

-   いずれかのターゲットをソース プロパティの一覧からの情報をコピーします。

コメント

-   参照してください[**センサー\_プロパティ\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)詳細についてはします。

**PropertiesListGetFillableCount**

センサー DDSI による使用量

-   特定のサイズのバッファーが保持できる可能性がある要素の数を返します。

コメント

-   なし。

## <a name="requirements"></a>要件


|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils.h         |

 

## <a name="related-topics"></a>関連トピック


[ヘルパー関数をマーシャ リング](marshalling-helper-functions.md)

 

 






