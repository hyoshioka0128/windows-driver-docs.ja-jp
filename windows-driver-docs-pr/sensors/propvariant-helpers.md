---
title: PropVariant ヘルパー
description: PropVariant ヘルパー関数は、センサーに関連付けられている PROPVARIANT 構造を操作するために v2 センサードライバーによって使用されます。
ms.assetid: 5A5A008A-399F-4464-ADD0-7F2DDACB6D4B
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 673d3c36291d9541ab4b212fee96a22f7212c2eb
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866770"
---
# <a name="sensor-propvariant-helpers"></a>センサー PropVariant ヘルパー

PropVariant ヘルパー関数は、センサーに関連付けられている[propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体を操作するために v2 センサードライバーによって使用されます。

ヘルパー関数は、センサーデバイスドライバーソフトウェアインターフェイス (DDSI) と共に使用されます。

| ヘルパー関数 | 操作 | コメント |
| --- | --- | --- |
| InitPropVariantFromFloat | [Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体を初期化します。 | この関数は FLOAT を受け取り、その変数に基づいて、 [Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体を作成して初期化します。 |
| PropKeyFindKeyGetPropVariant | [Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体を取得します。 | |
| PropKeyFindKeySetPropVariant | [Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体を設定します。 | |
| PropKeyFindKeyGetFileTime | データファイルに関連付けられているタイムスタンプを取得します。 |これは、指定されたプロパティキーに一致する[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体の*filetime*メンバーです。 |
| PropKeyFindKeyGetGuid | センサーの GUID を取得します。 | これは、指定されたプロパティキーに一致する[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体の*puuid*メンバーです。 |
| PropKeyFindKeyGetBool | センサーに関連付けられている[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体からブール値を取得します。 | |
| PropKeyFindKeyGetUlong | センサーに関連付けられている[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体から ULONG 値を取得します。 | |
| PropKeyFindKeyGetUshort | センサーに関連付けられている[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体から USHORT 値を取得します。 | |
| PropKeyFindKeyGetFloat | センサーに関連付けられている[propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体から FLOAT 値を取得します。 | |
| PropKeyFindKeyGetDouble | センサーに関連付けられている[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体から DOUBLE 値を取得します。 | |
| PropKeyFindKeyGetInt32 | センサーに関連付けられている[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体から32ビット値を取得します。 | |
| PropKeyFindKeyGetInt64 | センサーに関連付けられている[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体から64ビット値を取得します。 | |
| PropKeyFindKeyGetNthUlong | 指定されたプロパティキーに基づくコレクションリスト内の[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)から n 番目の ULONG 値を取得します。 | |
| PropKeyFindKeyGetNthUshort | 指定されたプロパティキーに基づくコレクションリスト内の[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)から n 番目の UShort 値を取得します。 | |
| PropKeyFindKeyGetNthInt64 | 指定されたプロパティキーに基づくコレクションリスト内の[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)から n 番目の Int64 値を取得します。 | |
| Isて Resentinpropertylist | ブール値を返します。 | ブール値は、センサーに関連付けられている[ **\_センサープロパティ\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)構造体でプロパティキーが見つかったかどうかを示します。|
| Isて Resentincollectionlist | ブール値を返します。 | ブール値は、プロパティキーが[ **\_センサーコレクション\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造で見つかったかどうかを示します。 センサーに関連付けられています。 |
| IsCollectionListSame | ブール値を返します。 | 2つ[**の\_センサー\_コレクションのリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)構造を比較して、両者が同じであるかどうかを確認します。 |
| PropVariantGetInformation | センサーに関連付けられている[Propvariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)構造体に関するサイズ、オフセット、およびその他の情報を取得します。 | |
| PropertiesListCopy | ソースプロパティリストからターゲット1に情報をコピーします。 | 詳細については、 [ **\_センサープロパティ\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)を参照してください。 |
|PropertiesListGetFillableCount | 特定のサイズのバッファーが保持できる可能性のある要素の数を返します。 | |

## <a name="requirements"></a>必要条件

|                          |                        |
|--------------------------|------------------------|
| サポートされている最小のクライアント | Windows 8.1            |
| サポートされている最小のサーバー | Windows Server 2012 R2 |
| Header                   | Sensorsutils         |

## <a name="related-topics"></a>関連トピック

[マーシャリングヘルパー関数](marshalling-helper-functions.md)
