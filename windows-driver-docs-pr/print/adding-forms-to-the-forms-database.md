---
title: フォーム データベースにフォームを追加する
description: フォーム データベースにフォームを追加する
ms.assetid: ac306f05-6150-4e47-9272-e81e658a1ea6
keywords:
- WDK Unidrv の追加フォーム
- Unidrv プリンター ドライバーへのフォームの追加
- Unidrv、データベースに追加するフォーム
- GPD ファイル WDK Unidrv、データベースに追加するフォーム
- プリンタ フォーム WDK
- フォームの WDK プリンター
- 特殊な形式の WDK プリンター
- 特殊な用紙サイズの WDK プリンター
- WDK のフォームの用紙サイズします。
- カスタム フォームの WDK プリンター
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ecb360b6f22e8154afd27a43fecbf21d0bfd35e
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349299"
---
# <a name="adding-forms-to-the-forms-database"></a>フォーム データベースにフォームを追加する


プリンターの追加フォームをサポートする場合は、プリンター ドライバーの GPD ファイルでそれらを記述することで Unidrv プリンター ドライバーを追加にできます。 リソース ID を使用する場合、 \*rcNameId フィールドと、フォームのリソース DLL 名の文字列を表示には、ドライバーは、Windows Vista Unidrv プリンター ドライバーを提供する新しいローカライズに関する拡張機能を自動的に使用します。 Unidrv プリンターのドライバー プラグインもスプーラーに自動的にこれらの変更を利用し、追加変更が必要としません。 これらの拡張機能の詳細については、次を参照してください。 [Windows Vista でプリンター フォームへの変更](changes-to-printer-forms-in-windows-vista.md)します。

GPD ファイル内のローカライズ可能な文字列のリソース DLL を使用していない場合は、ローカライズ可能な文字列を削除してリソース DLL に格納し、GPD ファイルに対応するリソース ID を文字列に 必要があります。

次のコード例は、表示名のリソース ID を使用する GPD ファイルから抜粋です。

```GDL
*Feature: PaperSize
{
    *Option: Option2
    {
 *rcNameID: 259
        (form definition)
    }
    (other form definitions).
}
```

Windows Vista では、フォームで提供される Unidrv プリンター ドライバー内で\_情報\_2 構造は次の表に示すように、GPD ファイルから読み取られるデータによって設定されます。 プリンター用 GPD ファイルが既にこの構造体を埋めるために必要な情報が含まれる場合は、Windows Vista Unidrv プリンター ドライバーを提供する新しい機能を使用する何も変更する必要はありません。

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

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>FORM_INFO_2 field</th>
<th>使用される GPD 値</th>
<th>フィールドの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>フラグ</p></td>
<td><p>FORM_PRINTER</p>
<p>この値は、フォームを追加しているため、Unidrv プリンター ドライバーによって割り当てられます。 GPD ファイルからの値は、このフィールドは使用されません。</p></td>
<td><p>構造のプロパティ。</p></td>
</tr>
<tr class="even">
<td><p>pName</p></td>
<td><p>リソース DLL から得られると、フォームのローカライズされた名前、* rcName GPD ファイルのフィールド。</p></td>
<td><p>フォームの名前を指定する null で終わる文字列へのポインター。 この文字列は、フォームのデータベース内のフォームを識別するために使用し、一意である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>サイズから読み取られた情報を * GPD ファイル PageDimensions オプション。</p></td>
<td><p>幅と高さをミリメートル単位のフォームの部分の 1/1000。</p></td>
</tr>
<tr class="even">
<td><p>ImageableArea</p></td>
<td><p>サイズから読み取られた情報を * GPD ファイル PrintableArea オプション。</p></td>
<td><p>幅と高さをミリメートル単位のプリンターが印刷できるページの領域の部分の 1/1000。</p></td>
</tr>
<tr class="odd">
<td><p>pKeyword</p></td>
<td><p>値、* GPD ファイル内のエントリのオプションします。</p></td>
<td><p>フォームのローカライズ文字列識別子へのポインター。 AddForm または SetForm に渡すと、このポインターはすべてのロケールでフォームを識別する方法を呼び出し元に示します。</p></td>
</tr>
<tr class="even">
<td><p>文字列型</p></td>
<td><p>STRING_MUIDLL</p>
<p>GPD で使用する場合、* rcNameId オプションとフォームの名前は、リソース DLL から使用可能な STRING_MUIDLL 値が割り当てられます。 場合、* rcName オプションを代わりに使用 GPD ファイルで、このフィールドの値は STRING_NONE します。 GPD ファイルからの値は、このフィールドは使用されません。</p></td>
<td><p>実行時にフォームのローカライズされた表示名を取得する方法を指定します。</p></td>
</tr>
<tr class="odd">
<td><p>pMuiDll</p></td>
<td><p>値、* GPD ResourceDLL エントリ ファイルの場合、* rcNameId オプションを使用します。 場合、* rcName オプションを代わりに使用 GPD ファイルで、このフィールドの値は<strong>NULL</strong>します。</p></td>
<td><p>ときに、この名前 MUI がローカライズされたリソースをローカライズされた表示を含む DLL<strong>文字列型</strong>STRING_MUIDLL が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>dwResourceId</p></td>
<td><p>値、*、GPD ファイル rcNameID エントリ。 場合、* rcName オプションを代わりに使用 GPD ファイルで、このフィールドの値は 0。</p></td>
<td><p>リソース ID で<strong>pMuiDll</strong>、フォームの表示のときに名前<strong>文字列型</strong>STRING_MUIDLL が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p>pDisplayName</p></td>
<td><p><strong>NULL</strong></p>
<p>このフィールドは使用されません。</p></td>
<td><p>言語では、フォームの表示名を<strong>wLangId</strong>タイミングを指定します<strong>文字列型</strong>STRING_LANGPAIR が含まれています。</p></td>
</tr>
<tr class="even">
<td><p>wLangId</p></td>
<td><p>0</p>
<p>このフィールドは使用されません。</p></td>
<td><p>言語<strong>pDisplayName</strong>とき<strong>文字列型</strong>STRING_LANGPAIR が含まれています。</p></td>
</tr>
</tbody>
</table>

 

 

 




