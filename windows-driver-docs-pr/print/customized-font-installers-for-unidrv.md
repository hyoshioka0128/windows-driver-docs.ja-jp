---
title: Unidrv 用にカスタマイズされたフォントインストーラー
description: Unidrv 用にカスタマイズされたフォントインストーラー
ms.assetid: d753368d-b1c8-454e-a02b-131dc778e723
keywords:
- WDK のカスタマイズ、コンポーネントのインストールに関するプリンタードライバー
- プリンタードライバーのカスタマイズ WDK、コンポーネントのインストール
- カスタムプリンタドライバコンポーネントのインストール (WDK)
- フォントインストーラー WDK Unidrv
- uff ファイル
- UFF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b847223b022e3b4eaa40afbcd4d9798db010ffb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837977"
---
# <a name="customized-font-installers-for-unidrv"></a>Unidrv 用にカスタマイズされたフォントインストーラー





製造元から提供されているフォントのインストールソフトウェアは、フォントカートリッジファイルによって記述されていないカートリッジフォントに必要です。 これらのフォントは、 [Unidrv フォントフォーマットファイル](customized-font-management.md#ddk-unidrv-font-format-files-gg)(uff ファイル) を使用して記述する必要があります。 Uff ファイルの作成は、ベンダーが提供するフォントインストーラーの役割を担います。

製造元から提供されているフォントインストーラーでは、ダウンロード可能な*PCL*ソフトフォントもサポートする必要があります。

カスタマイズされたフォントインストーラーを作成するには、次の2つの方法があります。

-   ユーザーインターフェイスプラグインを提供する

    このプラグインは、次の COM インターフェイスメソッドを実装する必要があります。

    [**IPrintOemUI:: Fontインストーラ Dlgproc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc)

    [**IPrintOemUI:: UpdateExternalFonts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts)

-   別の実行可能ファイルを指定する

    フォントのインストール中に、実行可能ファイルの名前をレジストリに格納する必要があります (Windows SDK のドキュメントで説明されています)。また、"FontInstaller" キーの値を指定します。

Unidrv は、次のアルゴリズムを使用してフォントインストーラーを検索します。

1.  フォントインストーラの実行可能ファイルの名前がレジストリに格納されている場合、システム管理者はプリンタのプロパティシートからフォントのインストール操作を選択できません。 代わりに、管理者は、指定された実行可能ファイルを実行する必要があります。

2.  インストーラーの実行可能ファイルが利用できない場合、Unidrv を使用すると、プリンターのプロパティシートからフォントのインストール操作を選択できます。 Unidrv は、ユーザーインターフェイスプラグインがインストールされているかどうかを判断します。 その場合は、そのフォントのインストール方法が呼び出されます。 ユーザーインターフェイスプラグインがインストールされていない場合、またはフォントのインストール方法で E\_NOTIMPL が返された場合、ドライバーは独自のエラーインストーラーを使用します。

 

 




