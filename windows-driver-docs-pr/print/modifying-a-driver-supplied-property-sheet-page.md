---
title: ドライバー提供のプロパティ シート ページを変更する
description: ドライバー提供のプロパティ シート ページを変更する
ms.assetid: 98338017-96a0-414c-9b80-bcb98eff61e5
keywords:
- ユーザーインターフェイスプラグイン WDK print、プロパティシートページ
- UI プラグイン WDK print、プロパティシートページ
- プロパティシートページの WDK 印刷
- オプション項目 WDK UI プラグイン
- カスタマイズされたオプション項目 WDK UI プラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8dfd87573164120f98db41aff140f85e7b1882c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824264"
---
# <a name="modifying-a-driver-supplied-property-sheet-page"></a>ドライバー提供のプロパティ シート ページを変更する





UI プラグインでは、 [**Iprintoemui:: CommonUIProp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッドとコールバック関数を実装することで、Unidrv または Pscript5 によって提供されるプロパティシートページを変更できます。

UI プラグインは**Iprintoemui:: CommonUIProp**メソッドを使用して、プリンターのプロパティシートの **[デバイスの設定]** ページまたはドキュメントのプロパティシートの **[レイアウト]** 、 **[用紙/品質]** 、 **[詳細設定**] の各ページで[CPSUI](common-property-sheet-user-interface.md)が追加、削除、または置換できるオプション項目のセットを指定します。

[**Oemcuipcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nc-printoem-oemcuipcallback)型のコールバック関数は、カスタマイズされたオプション項目に対するユーザーの変更を処理するために使用されます。

### <a href="" id="ddk-adding-option-items-gg"></a>オプション項目の追加

UI プラグインは、ドライバーによって提供される[**Optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)構造体の配列に配置することで、新しいオプション項目を記述する必要があります。 ドライバーのプリンターインターフェイス DLL は、UI プラグインの[**Iprintoemui:: CommonUIProp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッドを2回呼び出します。 メソッドを初めて呼び出すときは、必要な OPTITEM 構造体の数を返す必要があります。 このドライバーは、OPTITEM 配列に領域を割り当て、 [**Oemcuipparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam)構造体に配列を記述します。 ドライバーは、OEMCUIPPARAM 構造体のアドレスを指定して**Iprintoemui:: CommonUIProp**を再度呼び出します。そのため、メソッドは、オプションの説明を持つ optitem 構造体を読み込むことができます。

### <a href="" id="ddk-removing-option-items-gg"></a>削除 (オプション項目を)

Unidrv または Pscript5 によって提供されるプロパティシートページからオプションを削除するには、UI プラグインの[**Iprintoemui:: CommonUIProp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッドで、 [**Oemcuipparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam)構造体が指す[**optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)構造体の配列を走査することができます。 プロパティシートから削除するオプションごとに、OPTITEM 構造体の OPTITEM\_HIDE フラグを設定できます。 (これにより、このオプションは実際には削除されず、ユーザーが既定値を変更できないように、ユーザーのオプションは非表示になります)。

### <a href="" id="ddk-replacing-option-items-gg"></a>置換 (オプション項目を)

Unidrv または Pscript によって提供されるプロパティシートページのオプションを置き換えるには、前の「**オプション項目を削除**する」セクションに示されている手順に従って、既存のオプション項目を削除し、次の手順に従います。前に、**オプション項目**セクションを追加して、古い項目を置き換える新しいオプション項目を作成します。

### <a href="" id="ddk-handling-modifications-to-customized-option-values-gg"></a>カスタマイズされたオプション値に対する変更の処理

カスタマイズされたオプション項目に対するユーザーの変更を処理するには、少なくとも1つのコールバック関数を指定する必要があります。 ドキュメントプロパティシートとプリンタープロパティシートの両方のオプションを処理する1つのコールバック関数を指定するか、それぞれに個別の関数を指定することができます。 これらのコールバックの種類は、 [**Oemcuipcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nc-printoem-oemcuipcallback)です。

コールバック関数は、そのアドレスを[**Oemcuipparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam)構造体に配置することによって指定されます。 UI プラグインは、 [**Iprintoemui:: CommonUIProp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)メソッドへの入力として、この構造体のアドレスを受け取ります。

ユーザーがプリンターのプロパティシートまたはドキュメントのプロパティシートを開いてオプションを変更すると、 [CPSUI](common-property-sheet-user-interface.md)はプリンタードライバーのプリンターインターフェイス DLL を呼び出します。 この DLL は、独自の[**Optitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)構造体に含まれるオプション値を処理します。 次に、UI プラグインごとに、以前**Iprintoemui:: CommonUIProp**によって指定された OEMCUIPCALLBACK 型のコールバック関数を呼び出します。

 

 




