---
title: ドライバー提供のプロパティ シート ページを変更する
description: ドライバー提供のプロパティ シート ページを変更する
ms.assetid: 98338017-96a0-414c-9b80-bcb98eff61e5
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、プロパティ シート ページ
- UI プラグインを WDK の印刷、プロパティ シートのページ
- WDK プロパティ シートのページを印刷します。
- オプション アイテムを WDK UI プラグイン
- カスタマイズされたオプション項目を WDK UI プラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4c6b51a46a826f7bf6e2087ab82d85e52fa0a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384523"
---
# <a name="modifying-a-driver-supplied-property-sheet-page"></a>ドライバー提供のプロパティ シート ページを変更する





プラグイン UI は実装することで Unidrv 指定または Pscript5 提供のプロパティ シートのページを変更することができます、 [ **IPrintOemUI::CommonUIProp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッドとコールバック関数。

UI のプラグインで使用、 **IPrintOemUI::CommonUIProp**オプションのセットを指定するメソッドは項目を[CPSUI](common-property-sheet-user-interface.md)追加、削除、またはプリンターのプロパティ シートのいずれかで置き換えます**デバイス設定**ページまたはドキュメントのプロパティ シートの**レイアウト**、**用紙/品質**、および**詳細**ページ。

コールバック関数の型の[ **OEMCUIPCALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nc-printoem-oemcuipcallback)、カスタマイズされたオプション項目に対するユーザーの変更を処理するために使用します。

### <a href="" id="ddk-adding-option-items-gg"></a>オプションの項目の追加

UI プラグインはの配列に置くことで新しいオプション項目を記述する必要があります[ **OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)ドライバーによって提供される構造体。 ドライバーのプリンター インターフェイス DLL の呼び出しを UI プラグインの[ **IPrintOemUI::CommonUIProp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッドを 2 回です。 メソッドが呼び出されると、最初にその OPTITEM 構造が必要な数を返す必要があります。 ドライバー OPTITEM 配列の領域の割り当てし、で、配列を記述、 [ **OEMCUIPPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ns-printoem-_oemcuipparam)構造体。 ドライバー呼び出し**IPrintOemUI::CommonUIProp**オプションの説明をここでも、構造体 OEMCUIPPARAM 構造体のアドレスを指定するため、このメソッドは、OPTITEM を読み込むことができます。

### <a href="" id="ddk-removing-option-items-gg"></a>オプション項目を削除します。

Unidrv または Pscript5、UI プラグインでは、によって提供されるプロパティ シート ページからオプションを削除する[ **IPrintOemUI::CommonUIProp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッドの配列を走査できる[ **OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)によって示される構造体、 [ **OEMCUIPPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ns-printoem-_oemcuipparam)構造体。 OPTITEM 構造体の OPTIF を設定するプロパティ シートから削除したい各オプション\_非表示にするフラグ。 (注ことも実際には削除されませんオプションは、ユーザーがその既定値を変更できないように、ユーザーから、オプションの非表示になります)。

### <a href="" id="ddk-replacing-option-items-gg"></a>オプション アイテムを置き換える

Unidrv または Pscript によって指定されたプロパティ シート ページのオプションを置換する前に、下に表示する手順に従ってください**オプション項目を削除する**セクションに、既存のオプション項目を削除し、次の上記の指示**オプション項目の追加**古いものを置換する新しいオプション項目を作成します。

### <a href="" id="ddk-handling-modifications-to-customized-option-values-gg"></a>カスタマイズされたオプションの値の変更を処理

カスタマイズされたオプション項目に対するユーザーの変更を処理するために少なくとも 1 つのコールバック関数を提供する必要があります。 ドキュメントのプロパティ シートとプリンターのプロパティ シートの両方のオプションを処理する単一のコールバック関数を指定するか、またはごとの個別の関数を指定することができます。 これらのコールバックが型[ **OEMCUIPCALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/nc-printoem-oemcuipcallback)します。

コールバック関数がそのアドレスに配置することによって指定された、 [ **OEMCUIPPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ns-printoem-_oemcuipparam)構造体。 プラグインの UI では、この構造体のアドレスを受け取るへの入力としてその[ **IPrintOemUI::CommonUIProp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッド。

ユーザー プロパティ シートをプリンターまたはプロパティ シートのドキュメントを開くし、オプションを変更します[CPSUI](common-property-sheet-user-interface.md)プリンター インターフェイスのプリンター ドライバーの DLL を呼び出します。 この DLL は、独自に含まれるオプションの値を処理[ **OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)構造体。 各 UI プラグイン プリンター インターフェイス DLL の呼び出しによって以前に指定された OEMCUIPCALLBACK に型指定されたコールバック関数、 **IPrintOemUI::CommonUIProp**します。

 

 




