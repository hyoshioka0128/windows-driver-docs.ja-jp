---
title: COM ベースのレンダリング プラグイン
description: COM ベースのレンダリング プラグイン
ms.assetid: c80d6c2b-ba4d-4bd1-bd3a-8c1b0bf29884
keywords:
- COM ベースのレンダリングのプラグインを WDK の印刷
- COM ベースの印刷のプラグインを WDK のレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 306c004a28766a0d35f0244454715077256fd303
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369614"
---
# <a name="com-based-rendering-plug-ins"></a>COM ベースのレンダリング プラグイン





カスタマイズしたフック関数を提供するを実装する必要があります、COM ベースのレンダリング プラグイン、 [ **IPrintOemUni::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)または[ **IPrintOemPS::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enabledriver)を満たすメソッドを[ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)各フック関数のアドレスを持つ構造体。

Unidrv または Pscript5 ドライバーには、関数が定義されている場合にのみ、COM ベースのレンダリング プラグインできるグラフィックス DDI 関数をフックします。 このような関数の一覧は、次を参照してください。 [ **IPrintOemUni::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)または[ **IPrintOemPS::EnableDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enabledriver)します。

特定のカスタマイズのフック関数を指定すると、その関数は、ドライバーのと同じグラフィックス DDI 関数を横取りします。 カスタマイズされたフック関数を設計するときは、次のオプションがあります。

-   フック関数は、グラフィックス DDI 操作を内部的に処理することができます完全にします。

-   フック関数が、プリンター ドライバーのと同じグラフィックス DDI 関数にコールバックできます。

ドライバーのグラフィックス DDI 関数にコールバックしてフック関数は、前処理または関数の引数の後処理を実行がも、実際にグラフィック DDI 操作を実行するドライバーを許可します。 レンダリング プラグインでは、への入力引数の 1 つ[ **IPrintOemUni::EnablePDEV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)または[ **IPrintOemPS::EnablePDEV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-enablepdev)メソッドは、[ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)ドライバーのグラフィックス DDI 関数へのポインターを含む構造体。 これらの関数にコールバックする場合は、この構造体の内容を保存する必要があります。

提供するために必要な場合があります、 [PDEV 構造をカスタマイズ](customized-pdev-structures.md)します。 を通じてグラフィックス DDI のフック関数内からこの構造体を参照することができます、 [ **SURFOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_surfobj)各フック関数が入力として受け取る構造体のポインター。 具体的には、SURFOBJ 構造体の**dhpdev**へのポインターを[ **DEVOBJ** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ns-printoem-_devobj)構造、および DEVOBJ 構造体の**pdevOEM**メンバーは、カスタマイズされた PDEV 構造体を指します。

 

 




