---
title: テーブルのデータ ソースにおけるパラメーターの型
description: テーブルのデータ ソースにおけるパラメーターの型
ms.assetid: 034F171E-716F-4795-9B07-46A109052227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fd03548bd9009cfe6fb3208bcfc2da2a7020808
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425734"
---
# <a name="parameter-types-in-table-data-sources"></a>テーブルのデータ ソースにおけるパラメーターの型

次の表は、テーブルベースのデータソースで使用できるさまざまなパラメーター型の概要と、ネイティブ、マネージ、およびスクリプトの各テストでデータソースファイルの互換性を確保するために使用できる文字列の種類を示しています。

>[!NOTE]
>"String"、"int"、"bool"、"double"、" \_ \_ int64"、"unsigned \_ \_ int64"、および "XML" の各型は、すべてのマネージテスト、ネイティブテスト、またはスクリプトテストで使用できます。

既定では、型が指定されていない場合、型は "String" と見なされます。 各テーブルの最初の行を参照してください。

上で指定した型と共に配列型を指定するには、 \[ \] 型の末尾に "" を追加するだけです。

## <a name="for-native-tests"></a>ネイティブテストの場合

|ParameterType|言語の種類|
|----|----|
|文字列|WEX:: Common:: String|
|通り|INT|
|"unsigned int"|unsigned int|
|型|[bool]|
|小数|double|
|" \_ \_ int64"|\_\_int64|
|"unsigned \_ \_ int64"|符号なし \_ \_ int64|
|プロシージャ|DWORD|
|"size \_ t"|サイズ \_ t|
|"NoThrowString"|WEX:: Common:: NoThrowString|
|XML|WEX:: Common:: String|

## <a name="for-managed-tests"></a>マネージテストの場合

|ParameterType|言語の種類|
|----|----|
|文字列|string|
|"Int32" または "int"|INT|
|"uint" または "uint32"|uint|
|"bool" または "boolean"|[bool]|
|"double" または "decimal"|decimal|
|" \_ \_ int64" または "int64"|int64|
|"unsigned \_ \_ int64" または "uint64"|uint64|
|プロシージャ|uint|
|XML|string|

## <a name="for-script-tests"></a>スクリプトテストの場合

|ParameterType|言語の種類|
|----|----|
|"String" または "BSTR"|VT \_ BSTR|
|通り|VT \_ INT|
|"unsigned int" または "uint"|VT \_ UINT|
|型|VT \_ BOOL|
|小数|VT \_ R8|
|" \_ \_ int64"|VT \_ I8|
|"unsigned \_ \_ int64"|VT \_ UI8|
|XML|VT \_ BSTR|
