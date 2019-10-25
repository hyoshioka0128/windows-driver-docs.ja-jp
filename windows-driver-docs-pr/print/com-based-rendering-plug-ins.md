---
title: COM ベースのレンダリング プラグイン
description: COM ベースのレンダリング プラグイン
ms.assetid: c80d6c2b-ba4d-4bd1-bd3a-8c1b0bf29884
keywords:
- COM ベースのレンダリングプラグインの WDK 印刷
- レンダリングプラグイン WDK print、COM ベース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 875f69820cd46736e7236ac76ae1e9dd272266dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842874"
---
# <a name="com-based-rendering-plug-ins"></a>COM ベースのレンダリング プラグイン





カスタマイズされたフック関数を提供するには、COM ベースのレンダリングプラグインで[**Iprintoemuni:: enabledriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)メソッドまたは[**IPrintOemPS:: enabledriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)メソッドを実装する必要があります。これにより、 [**dr abledata**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)構造体にそれぞれのアドレスが設定されます。フック関数。

COM ベースのレンダリングプラグインは、Unidrv または Pscript5 ドライバーで関数が定義されている場合にのみ、グラフィックス DDI 関数をフックできます。 このような関数の一覧については、「 [**Iprintoemuni:: enabledriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)または[**IPrintOemPS:: enabledriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enabledriver)」を参照してください。

特定のカスタマイズされたフック関数を指定した場合、その関数は、ドライバーの同等のグラフィックス DDI 関数をプリエンプションします。 カスタマイズしたフック関数を設計するときは、次のオプションがあります。

-   フック関数は、グラフィックスの DDI 操作を内部で完全に処理できます。

-   フック関数は、プリンタードライバーに相当するグラフィックス DDI 関数にコールバックできます。

ドライバーの graphics DDI 関数にコールバックすることによって、フック関数は関数の引数の前処理または後処理を実行できますが、ドライバーは実際にはグラフィックスの DDI 操作を実行できます。 レンダリングプラグインの[**Iprintoemuni:: enablepdev**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)メソッドまたは[**IPrintOemPS:: enablepdev**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-enablepdev)メソッドへの入力引数の1つは、ドライバーの graphics DDI 関数へのポインターを含む[**drvenabledata**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)構造体です。 これらの関数にコールバックする場合は、この構造体の内容を保存する必要があります。

カスタマイズされた[PDEV 構造](customized-pdev-structures.md)を提供する必要がある場合があります。 この構造体は、各フック関数が入力として受け取る、次のよう[**に、グラフィックの DDI**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj)フック関数内から参照できます。 具体的には、のように、は、"、" というように、ユーザーが指定し**た PDEV**構造体を参照している場合、**このメンバーは**、"、"[**というよう**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_devobj)に指定します。

 

 




