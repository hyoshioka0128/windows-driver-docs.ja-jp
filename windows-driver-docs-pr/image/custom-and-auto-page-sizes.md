---
title: カスタムおよび自動のページ サイズ
description: カスタムおよび自動のページ サイズ
ms.assetid: a1f5f78d-fc05-4a7e-9d19-c7f40302b85f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a91fbc8f2a0483b7134f2f392dcca78c773e0703
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840862"
---
# <a name="custom-and-auto-page-sizes"></a>カスタムおよび自動のページ サイズ


アプリケーションでは、スキャナーによる自動検出またはカスタム値を使用して、ページサイズを設定できます。 アプリケーションによって使用されるアプローチは、 [**wia\_ip\_ページ\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-page-size)プロパティによって決定されます。このプロパティは、[\_\_] ページ\_[自動] または [wia\_] ページ [カスタム] の値を取ることができます。

アプリケーションで WIA\_IP\_ページ\_サイズが WIA\_PAGE\_CUSTOM 以外の値に設定されている場合、WIA ミニドライバーは、wia\_IP\_ページ\_WIDTH と WIA の値を調整する必要があり\_IPS\_ページの高さは、ページのディメンションに対して、1000インチ (001) 単位で\_ます。 また、ミニドライバーでは、WIA\_IP\_XEXTENT と WIA\_\_IP の値をページのサイズ (ピクセル単位) に調整する必要があります。

エクステント設定 (WIA\_IP\_XEXTENT または WIA\_IP\_YEXTENT) が、現在のページサイズ設定と一致し*ない*値に変更された場合、ミニドライバーは、WIA\_IPS\_ページの値を変更する必要があり\_SIZE プロパティを WIA\_ページ\_カスタムに設定します。 また、ミニドライバーは、新しいエクステントの設定に同意するために、\_ページ\_幅または WIA\_IP\_ページの高さを\_変更する必要があります。

アプリケーションで WIA\_IP\_ページ\_SIZE プロパティを WIA\_PAGE\_CUSTOM に設定した場合、現在の選択領域は影響を受けません。 WIA ミニドライバーは、現在のイメージのレイアウトを取得する必要があります。これは、 [**wia\_ips\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)および[**wia\_ip\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)プロパティの現在の設定から開始します。 ページサイズの設定によって、選択領域がスキャナーのベッドの外にある場合、ミニドライバーは、WIA\_IPS\_XPOS および WIA\_IP\_YPOS プロパティの値を有効な設定に自動的に調整する必要があります。 WIA\_IP\_ページ\_SIZE と WIA\_IP\_方向のプロパティが同時に設定され、それらが組み合わせて適用されている場合は無効になるため、ミニドライバーは、アプリケーションの設定を[**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)メソッドでエラーが発生しています。

ページサイズの自動検出が有効になっている場合、ドライバーは、イメージデータの転送が完了した後にのみ、正確な画像のディメンション情報を提供する必要があります。 ストリームベースの転送の場合、ドライバーは、転送の終了時にイメージヘッダー内のイメージのサイズを更新する必要があります。 新しいセッションの開始時に、WIA\_IP\_ページ\_SIZE プロパティの値は、常に、WIA\_PAGE\_AUTO 以外の値に設定する必要があります。

WIA\_PAGE\_AUTO が現在の WIA\_IP\_PAGE\_SIZE 値として設定されている場合、ドライバーはまず汎用画像ディメンションを含むイメージヘッダーを転送し、次に画像データを転送する必要があります。次に、転送ストリームの先頭に戻り、イメージヘッダーを (スキャン完了後に検出された) 実際のイメージディメンションで更新し、ストリームのインデックスをストリームの末尾に戻します。

WIA\_PAGE\_AUTO が設定されている場合 (ドライバーによって既定値として選択されているか、アプリケーションによって設定された場合)、イメージの転送全体が完了するまで、アプリケーションはイメージヘッダーに記述されているイメージのサイズを処理しないようにする必要があります。

**ただし**、wia サービス内の互換性レイヤーでは、プロパティが WINDOWS XP wia デバイスから変換される ADF 項目に対する\_IP\_ページ\_サイズのサポートは追加されません。プロパティがの子項目でサポートされていない場合は、  ます。ドライブ. アプリケーションでは、ADF 項目が常にこのプロパティをサポートしているとは限りません。実行時に、WIA\_IP\_ページ\_サイズがサポートされているかどうかを常に確認する必要があります。 (通常、アプリケーションは、ネゴシエートされるプロパティのサポートを確認する必要があります)。

 

 

 




