---
title: Unidrv のカスタマイズされたフォント インストーラー
description: Unidrv のカスタマイズされたフォント インストーラー
ms.assetid: d753368d-b1c8-454e-a02b-131dc778e723
keywords:
- プリンター ドライバー WDK のカスタマイズ、コンポーネントをインストールします。
- プリンター ドライバー WDK、コンポーネントのインストールをカスタマイズします。
- カスタムのプリンター ドライバー コンポーネント WDK をインストールします。
- フォントのインストーラー WDK Unidrv
- .uff ファイル
- UFF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca8548adb5ef53b60f9d671b8dd39c6b3e2de81a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372406"
---
# <a name="customized-font-installers-for-unidrv"></a>Unidrv のカスタマイズされたフォント インストーラー





フォントのベンダーから提供されたインストール ソフトウェアは、フォントのカートリッジ ファイルで説明されていないカートリッジ フォントに必要です。 使用してこれらのフォントを記述する必要があります[Unidrv フォント形式ファイル](customized-font-management.md#ddk-unidrv-font-format-files-gg)(.uff ファイル)。 .Uff ファイルの作成は、フォントのベンダーから提供されたインストーラーの責任です。

フォントのベンダーから提供されたインストーラーは、サポートを提供する必要がありますもダウンロード可能な*PCL*ソフト フォント。

フォントのカスタマイズされたインストーラーを作成する 2 つの手法は次のとおりです。

-   プラグインのユーザー インターフェイスを提供します。

    次の COM インターフェイス メソッドは、このプラグインの場合に実装する必要があります。

    [**IPrintOemUI::FontInstallerDlgProc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc)

    [**IPrintOemUI::UpdateExternalFonts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts)

-   別の実行可能ファイルを指定します。

    フォントのインストール中に、実行可能ファイルする必要があります、名前、レジストリに格納 SetPrinterData (Windows SDK のドキュメントで説明) を呼び出すことによって、"FontInstaller"キーの値を指定します。

Unidrv は、フォント インストーラーを検索するため、次のアルゴリズムを使用します。

1.  フォントのインストーラー実行可能ファイルの名前がレジストリに格納されている場合、Unidrv はプリンターのプロパティ シートからフォントのインストールの操作を選択するシステム管理者を許可しません。 代わりに、管理者は、指定された実行可能ファイルを実行する必要があります。

2.  インストーラーの実行可能ファイルが利用できない場合、Unidrv には、プリンターのプロパティ シートからフォントのインストール操作の選択ができるようにします。 Unidrv は、ユーザー インターフェイスのプラグインがインストールされているかどうかを決定します。 そうである場合は、そのフォントのインストール方法が呼び出されます。 ユーザー インターフェイスのプラグインがインストールされていない場合、またはそのフォントのインストール方法が返す E\_NOTIMPL、ドライバーは、独自の障害のインストーラーを使用します。

 

 




