---
title: TVOT\_プッシュボタン
description: TVOT\_プッシュボタン
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
ms.openlocfilehash: b9360209d5c6f455f174f7877569eebed57adc6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845250"
---
# <a name="tvot_pushbutton"></a>TVOT\_プッシュボタン


## <span id="ddk_tvot_pushbutton_gg"></span><span id="DDK_TVOT_PUSHBUTTON_GG"></span>


TVOT\_のプッシュボタンオプションの種類は、グループボックス内のプッシュボタンで構成されています。

<span id="OPTITEM_Structure"></span><span id="optitem_structure"></span><span id="OPTITEM_STRUCTURE"></span>[**Optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)データ  

<span id="Sel_pSel"></span><span id="sel_psel"></span><span id="SEL_PSEL"></span>**Sel/pSel**  
次のように、OPTPARAM 構造体の**スタイル**メンバーに依存します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プッシュボタンのスタイル</th>
<th>Sel/pSel の使用状況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>使用しません。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>CPSUI は、ダイアログボックスプロシージャの戻り値を格納します。</p></td>
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

 

<span id="OPTPARAM_Structure_Array__pOptParam_member_of_OPTTYPE_"></span><span id="optparam_structure_array__poptparam_member_of_opttype_"></span><span id="OPTPARAM_STRUCTURE_ARRAY__POPTPARAM_MEMBER_OF_OPTTYPE_"></span>[**Optparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam)構造体配列 ( [**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)の**poptparam**メンバー)  

<span id="pData"></span><span id="pdata"></span><span id="PDATA"></span>**pData**  
次のように、**スタイル**メンバーによって異なります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プッシュボタンのスタイル</th>
<th>pData の使用状況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)"><strong>_CPSUICALLBACK</strong></a>で型指定された関数へのポインター。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>DLGPROC によって入力されたダイアログボックスプロシージャへのポインター (Microsoft Windows SDK のドキュメントを参照)。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>COLORADJUSTMENT 構造へのポインター (Windows SDK のドキュメントを参照)。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_devhtadjdata" data-raw-source="[&lt;strong&gt;DEVHTADJDATA&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_devhtadjdata)"><strong>DEVHTADJDATA</strong></a>構造体へのポインター。</p></td>
</tr>
</tbody>
</table>

 

<span id="IconID"></span><span id="iconid"></span><span id="ICONID"></span>**IconID**  
プッシュボタンに関連付けられるアイコンを識別します。

<span id="___________lParam__________"></span><span id="___________lparam__________"></span><span id="___________LPARAM__________"></span>lParam   
次のように、スタイルメンバーによって異なります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プッシュボタンのスタイル</th>
<th>lParam の使用状況</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>使用しません。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>ダイアログリソースのリソース識別子。または、DLGTEMPLATE 構造体を識別するハンドル (Windows SDK のドキュメントを参照してください)。 OPTPARAM 構造体の<strong>Flags</strong>メンバーの DPF_USE_HDLGTEMPLATE フラグに依存します。</p></td>
</tr>
<tr class="odd">
<td><p>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>使用しません。</p></td>
</tr>
<tr class="even">
<td><p>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>使用しません。</p></td>
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
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span>スタイル</p></td>
<td><p>ユーザーがプッシュボタンをクリックしたときに CPSUI によって実行される操作を指定します。 次のいずれかの値を指定できます。</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_CALLBACK"></span><span id="pushbutton_type_callback"></span>PUSHBUTTON_TYPE_CALLBACK</p></td>
<td><p>CPSUI は、アプリケーションの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback" data-raw-source="[&lt;strong&gt;_CPSUICALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/nc-compstui-_cpsuicallback)"><strong>_CPSUICALLBACK</strong></a>で型指定されたコールバック関数を呼び出して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam)"><strong>Cpsuicbparam</strong></a>構造体の<strong>Reason</strong>メンバーを CPSUICB_REASON_PUSHBUTTON に設定して、ボタンイベントを処理します。 (CPSUI は、コールバック関数の戻り値を無視します)。</p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_DLGPROC"></span><span id="pushbutton_type_dlgproc"></span>PUSHBUTTON_TYPE_DLGPROC</p></td>
<td><p>アプリケーションのダイアログボックスプロシージャは、ボタンイベントを処理します。 (詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage" data-raw-source="[&lt;strong&gt;DLGPAGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)"><strong>Dlgpage</strong></a>」の「<strong>解説</strong>」を参照してください)。</p>
<p>関数が WM_INITDIALOG メッセージを受信すると、その<em>lParam</em>引数は、 <strong>REASON</strong>メンバーが CPSUICB_REASON_DLGPROC に設定された<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam" data-raw-source="[&lt;strong&gt;CPSUICBPARAM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_cpsuicbparam)"><strong>cpsuicbparam</strong></a>構造体を指します。</p></td>
</tr>
<tr class="even">
<td><p><span id="PUSHBUTTON_TYPE_HTCLRADJ"></span><span id="pushbutton_type_htclradj"></span>PUSHBUTTON_TYPE_HTCLRADJ</p></td>
<td><p>CPSUI ハーフトーンの色調整ダイアログボックスを表示します。</p></td>
</tr>
<tr class="odd">
<td><p><span id="PUSHBUTTON_TYPE_HTSETUP"></span><span id="pushbutton_type_htsetup"></span>PUSHBUTTON_TYPE_HTSETUP</p></td>
<td><p>CPSUI [デバイスハーフトーンの設定] ダイアログボックスが表示されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="OPTTYPE_Structure"></span><span id="opttype_structure"></span><span id="OPTTYPE_STRUCTURE"></span>[**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)データ  

<span id="___________Type__________"></span><span id="___________type__________"></span><span id="___________TYPE__________"></span>各種   
TVOT\_プッシュボタン

<span id="___________Count__________"></span><span id="___________count__________"></span><span id="___________COUNT__________"></span>数   
1

<span id="___________Style__________"></span><span id="___________style__________"></span><span id="___________STYLE__________"></span>スタイル   
次のオプションのビットフラグを指定できます。

<span id="OTS_PUSH_ENABLE_ALWAYS"></span><span id="ots_push_enable_always"></span>OTS\_PUSH\_有効にする\_常に  
設定すると、ユーザーがプロパティシートページを変更できない場合でも、プッシュボタンは常に有効になります (つまり、 [**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)構造体で CPSUIF\_UPDATE\_権限が設定されていない場合でも)。

プッシュボタンのコールバック関数は、そのダイアログを表示する必要がありますが、ユーザーが変更できないようにする必要があります。

注: このフラグは、 [**Opttype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)構造体の**Flags**メンバーでも設定する必要があります。

<span id="OTS_PUSH_INCL_SETUP_TITLE"></span><span id="ots_push_incl_setup_title"></span>\_セットアップ\_タイトルを含む\_プッシュ\_  
設定した場合、CPSUI には、ボタンの名前文字列の後に "Setup" という単語が含まれます (OPTITEM では**pName** )。

<span id="OTS_PUSH_NO_DOT_DOT_DOT"></span><span id="ots_push_no_dot_dot_dot"></span>OTS\_PUSH\_\_DOT\_dot\_dot  
設定した場合、CPSUI には、ボタンの名前文字列 (OPTITEM では**pName** ) の後に3つのドット (...) が含まれます。

<span id="BegCtrlID"></span><span id="begctrlid"></span><span id="BEGCTRLID"></span>**BegCtrlID**  
[**COMPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui)の**pDlgPage**が CPSUI 提供のページを識別する場合、または[**DLGPAGE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_dlgpage)の**DlgTemplateID**が CPSUI で提供されるテンプレートを識別する場合、 **begctrlid**は使用されません。

それ以外の場合、 **Begctrlid**には、順番に番号が付けられた一連のコントロール id の最初のコントロール識別子が含まれている必要があります。 コントロール識別子は、次の Windows コントロールを識別する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コントロール識別子</th>
<th>Windows コントロール</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Begctrlid</strong>の内容</p></td>
<td><p>グループボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>Begctrlid</strong>コンテンツ + 1</p></td>
<td><p>タイトルのテキスト</p></td>
</tr>
<tr class="odd">
<td><p><strong>Begctrlid</strong>コンテンツ + 2</p></td>
<td><p>プッシュボタンボックス</p></td>
</tr>
<tr class="even">
<td><p><strong>Begctrlid</strong>コンテンツ + 3</p></td>
<td><p>プッシュボタンアイコン</p></td>
</tr>
<tr class="odd">
<td><p><strong>Begctrlid</strong>コンテンツ + 4</p></td>
<td><p>拡張チェックボックスまたは拡張プッシュボタン (オプション)</p></td>
</tr>
<tr class="even">
<td><p><strong>Begctrlid</strong>コンテンツ + 5</p></td>
<td><p>拡張チェックボックスまたは拡張プッシュボタンアイコン (省略可能)</p></td>
</tr>
</tbody>
</table>

 

詳細については、「 [CPSUI でサポートされているウィンドウコントロールのカスタマイズ](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-cpsui-supported-window-controls)」を参照してください。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Compstui (Compstui を含む)</td>
</tr>
</tbody>
</table>

 

 




