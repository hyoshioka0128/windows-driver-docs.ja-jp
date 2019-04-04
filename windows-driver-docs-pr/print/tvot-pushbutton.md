---
title: TVOT\_プッシュ ボタン
description: TVOT\_プッシュ ボタン
ms.assetid: 47d51066-c1bc-4a84-bc9b-5091100b9f53
keywords:
- TVOT_PUSHBUTTON 印刷デバイス
topic_type:
- apiref
api_name:
- TVOT_PUSHBUTTON
api_location:
- compstui.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36ec2aa2eef0f29371e670ef7f06c7a40dd49478
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349217"
---
# <a name="tvotpushbutton"></a>TVOT\_プッシュ ボタン


## <span id="ddk_tvot_pushbutton_gg"></span><span id="DDK_TVOT_PUSHBUTTON_GG"></span>


TVOT\_プッシュ ボタンのオプションの種類は、グループ ボックス内でのプッシュ ボタンで構成されています。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)構造体  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
依存、**スタイル**次のように、OPTPARAM$ のメンバーが構造体します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プッシュ ボタンのスタイル</th>
<th>Sel pSel/使用状況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>使用されません。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>CPSUI では、ダイアログ ボックス プロシージャの戻り値を格納します。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>CPSUI は、ハーフトーン操作の戻り値を格納します。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>CPSUI は、ハーフトーン操作の戻り値を格納します。</p></td>
</tr>
</tbody>
</table>

 

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**OPTPARAM$** ](https://msdn.microsoft.com/library/windows/hardware/ff559660)構造体の配列 (**pOptParam**のメンバー [ **OPTTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff559670))  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
依存、**スタイル**メンバーは、次のようにします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プッシュ ボタンのスタイル</th>
<th>pData の使用状況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff564313" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564313)"> <strong>_CPSUICALLBACK</strong></a>-関数の型を指定します。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>ダイアログ ボックス プロシージャ DLGPROC に型指定されたポインター (Microsoft Windows SDK のドキュメントを参照してください)。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>(Windows SDK のドキュメントで説明) COLORADJUSTMENT 構造体へのポインター。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff552832" data-raw-source="[&lt;strong&gt;DEVHTADJDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552832)"> <strong>DEVHTADJDATA</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
プッシュ ボタンに関連付けるアイコンを識別します。

<span id="___________lParam__________"></span><span id="___________lparam__________"></span><span id="___________LPARAM__________"></span> lParam   
次のように、スタイルのメンバーに依存します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プッシュ ボタンのスタイル</th>
<th>lParam 使用状況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>使用されません。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>ダイアログ リソース、または DLGTEMPLATE 構造体へのハンドルのリソース識別子 (Windows SDK のドキュメントを参照してください)。 OPTPARAM$ 構造体の DPF_USE_HDLGTEMPLATE フラグによって異なります<strong>フラグ</strong>メンバー。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>使用されません。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>使用されません。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span> スタイル</p></td>
<td><p>ユーザーがプッシュ ボタンをクリックすると、CPSUI により実行される操作を指定します。 次のいずれかの値になります。</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_CALLBACK"></span><span id="pushbutton_type_callback"></span>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>CPSUI 呼び出し、アプリケーションの<a href="https://msdn.microsoft.com/library/windows/hardware/ff564313" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564313)"> <strong>_CPSUICALLBACK</strong></a>-コールバック関数をボタンのイベントを処理するために型指定された、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547088" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547088)"> <strong>CPSUICBPARAM</strong> </a>構造体の<strong>理由</strong>メンバー CPSUICB_REASON_PUSHBUTTON に設定します。 (CPSUI は、コールバック関数の戻り値を無視します)。</p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_DLGPROC"></span><span id="pushbutton_type_dlgproc"></span>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>アプリケーションのダイアログ ボックス プロシージャでは、ボタンのイベントを処理します。 (詳細については、次を参照してください、<strong>解説</strong>セクション<a href="https://msdn.microsoft.com/library/windows/hardware/ff547607" data-raw-source="[&lt;strong&gt;DLGPAGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547607)"> <strong>DLGPAGE</strong></a>。)。</p>
<p>関数は、WM_INITDIALOG メッセージを受信するときにその<em>lParam</em>引数が指す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff547088" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547088)"> <strong>CPSUICBPARAM</strong> </a>構造体、<strong>理由</strong>メンバー CPSUICB_REASON_DLGPROC に設定します。</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_HTCLRADJ"></span><span id="pushbutton_type_htclradj"></span>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>CPSUI は、ハーフトーン色の調整 ダイアログ ボックスが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_HTSETUP"></span><span id="pushbutton_type_htsetup"></span>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>CPSUI では、デバイス ハーフトーンのセットアップ ダイアログ ボックスが表示されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体  

<span id="___________Type__________"></span><span id="___________type__________"></span><span id="___________TYPE__________"></span> 型   
TVOT\_プッシュ ボタン

<span id="___________Count__________"></span><span id="___________count__________"></span><span id="___________COUNT__________"></span> カウント   
1

<span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span> スタイル   
次のオプションのビット フラグを指定することができます。

<span id="OTS_PUSH_ENABLE_ALWAYS"></span><span id="ots_push_enable_always"></span>OTS\_プッシュ\_を有効にする\_常に  
かどうか設定すると、プッシュ ボタンは常に有効、ユーザーは、プロパティ シート ページを変更できない場合でも (つまり場合でも CPSUIF\_UPDATE\_アクセス許可が設定されていない、 [ **COMPROPSHEETUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546211)構造)。

プッシュ ボタンのコールバック関数は、ダイアログ ボックスで、表示する必要がありますが、ユーザーによる変更をすることはできません。

注: このフラグを設定する必要がありますも、**フラグ**のメンバー、 [ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)構造体。

<span id="OTS_PUSH_INCL_SETUP_TITLE"></span><span id="ots_push_incl_setup_title"></span>OTS\_プッシュ\_含める\_セットアップ\_タイトル  
設定すると、CPSUI が含まれるかどうか、単語「セットアップ」、ボタンの名前の文字列の後 (**pName** OPTITEM で)。

<span id="OTS_PUSH_NO_DOT_DOT_DOT"></span><span id="ots_push_no_dot_dot_dot"></span>OTS\_プッシュ\_いいえ\_ドット\_ドット\_ドット  
かどうか設定、CPSUI 後を含む 3 つのドット (...) ボタンの名前の文字列 (**pName** OPTITEM で)。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
場合**pDlgPage**で[ **COMPROPSHEETUI** ](https://msdn.microsoft.com/library/windows/hardware/ff546211) CPSUI が指定したページを識別する場合、または**DlgTemplateID**で[ **DLGPAGE** ](https://msdn.microsoft.com/library/windows/hardware/ff547607) CPSUI が指定したテンプレートでは、識別**BegCtrlID**は使用されません。

それ以外の場合、 **BegCtrlID**順番に番号付きの一連のコントロール id の最初のコントロールの識別子を含める必要があります。 コントロールの id は、次の Windows コントロールを識別する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コントロールの識別子</th>
<th>Windows コントロール</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容</p></td>
<td><p>グループ ボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容は + 1</p></td>
<td><p>タイトルのテキスト</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容 + 2</p></td>
<td><p>プッシュ ボタン ボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 3</p></td>
<td><p>プッシュ ボタンのアイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>BegCtrlID</strong>内容は + 4</p></td>
<td><p>チェック ボックスを拡張または拡張のプッシュ ボタン (省略可能)</p></td>
</tr>
<tr class="even">
<td><p><strong>BegCtrlID</strong>内容 + 5</p></td>
<td><p>チェック ボックスを拡張または拡張ボタンのアイコン (省略可能)</p></td>
</tr>
</tbody>
</table>

 

詳細については、[Customizing CPSUI-Supported ウィンドウ コントロール](https://msdn.microsoft.com/library/windows/hardware/ff547296)を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Compstui.h (include Compstui.h)</td>
</tr>
</tbody>
</table>

 

 




