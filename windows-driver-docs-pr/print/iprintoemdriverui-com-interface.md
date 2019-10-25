---
title: IPrintOemDriverUI COM インターフェイス
description: IPrintOemDriverUI COM インターフェイス
ms.assetid: ed11789f-750d-4f29-b5e0-ab299a1388db
keywords:
- IPrintOemDriverUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b5a5ef7a852c02b5594e2fe4bd63a44e4f21801
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844325"
---
# <a name="iprintoemdriverui-com-interface"></a>IPrintOemDriverUI COM インターフェイス





`IPrintOemDriverUI` COM インターフェイスを使用すると、UI プラグインは、Unidrv または Pscript の[プリンターインターフェイス DLL](printer-interface-dll.md)によって管理される情報を表示および変更できます。

次の表に、`IPrintOemDriverUI` インターフェイスで定義されているすべてのメソッドの一覧とその説明を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvGetDriverSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting)"><strong>IPrintOemDriverUI::D rvGetDriverSetting</strong></a></p></td>
<td><p>UI プラグインを使用して、プリンター機能の現在の状態とその他の内部情報を取得できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvUpdateUISetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)"><strong>IPrintOemDriverUI::D rvUpdateUISetting</strong></a></p></td>
<td><p>UI プラグインが、変更されたユーザーインターフェイスオプションをドライバーに通知できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvUpgradeRegistrySetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting)"><strong>IPrintOemDriverUI::D rvUpgradeRegistrySetting</strong></a></p></td>
<td><p>UI プラグインがレジストリに格納されているデバイス設定を更新できるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 




