---
title: FORM_INFO_2 データ構造
description: FORM_INFO_2 データ構造
ms.assetid: df953fe9-00a2-468a-a2ae-ba8f3fce9982
keywords:
- FORM_INFO_2 データ構造の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d175c3ba4212fc0382702b3d31855c78bd2511
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363230"
---
# <a name="forminfo2-data-structure"></a>フォーム\_情報\_2 つのデータ構造体


多言語環境でのプリンター フォーム サポートの向上を提供する Windows Vista では、印刷スプーラーおよび Unidrv プリンター ドライバーが強化されています。 スプーラーは、フォームの表示名と新しいフォームの複数言語ユーザー インターフェイス (MUI) の文字列をサポートしている\_情報\_2 つのデータ構造の MUI 文字列をサポートするために必要な追加情報が含まれます。

フォーム\_情報\_1 のデータ構造は次のように定義されます。

```cpp
typedef struct _FORM_INFO_1 { 
  DWORD  Flags; 
  LPTSTR  pName; 
  SIZEL   Size; 
  RECTL   ImageableArea; 
} FORM_INFO_1, *PFORM_INFO_1;
```

フォームで\_情報\_1、pName メンバーが唯一の文字列フィールド名を作成するキーを内部データベースにフォームを見つけて、名前、表示としても、内部検索ルーチンを使用するエンドユーザーに表示される使用できるようにします。

フォーム\_情報\_次のコード例で定義されている 2 つの構造体には、MUI をサポートするフィールドが追加されます。

```cpp
typedef struct _FORM_INFO_2 { 
  DWORD    Flags; 
  LPTSTR   pName; 
  SIZEL    Size; 
  RECTL    ImageableArea;
  LPCSTR   pKeyword;
  DWORD    StringType;
  LPCTSTR  pMuiDll;
  DWORD    dwResourceId;
  LPCTSTR  pDisplayName;
  LANGID   wLangId; 
} FORM_INFO_2, *PFORM_INFO_2;
```

フォーム\_情報\_2 は distinct キーワード、表示名と異なることができる 1 つの追加を有効にする pKeyword メンバーを追加します。

この構造体を使用して、pMuiDll と dwResourceId メンバーを使用して、フォームのデータベースをリソース DLL とリソース ID を追加することもできます。 文字列型のメンバーが文字列の値を持っている場合\_MUIDLL と pMuiDll と dwResourceId のメンバーは、リソース DLL と、表示名の識別子が含まれて、 **AddForm**スプーラーの関数は、表示DLL の名前が内部的に記録します。 2、形式で返される情報のレベルの値を持つ GetForm または EnumForms 関数を呼び出すときに\_情報\_2 構造には、その pDisplayName 参照と、対応する言語の ID の表示名にが含まれますwLangID します。

フォームを使用するプリンター ドライバー\_情報\_1 構造 AddForm の呼び出し時にフォームのデータベースでは、その構造に含まれる情報のみが保存されます。 フォーム内のメンバー\_情報\_2 構造形式ではない\_情報\_1 構造になります**NULL**または GetForm またはフォームが返す EnumForms への呼び出しでクエリを実行するときは 0\_情報\_2 構造体。

プリンター フォームを追加する方法と、フォームの使用方法の詳細については\_情報\_1 とフォーム\_情報\_2 つのデータ構造体は、Microsoft Windows SDK のマニュアルを参照してください。

 

 




