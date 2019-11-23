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

アプリケーションで WIA\_IP\_\_ページのサイズを WIA\_PAGE\_CUSTOM 以外の値に設定した場合、wia ミニドライバーでは、wia\_IP\_ページ\_の幅と WIA\_IP\_ページの高さを、ページのサイズに対して1000分の1インチ (001) で調整する必要があります。\_ また、ミニドライバーでは、WIA\_IP\_XEXTENT と WIA\_\_IP の値をページのサイズ (ピクセル単位) に調整する必要があります。

エクステントの設定 (WIA\_IP\_XEXTENT または WIA\_IP\_YEXTENT) が、現在のページサイズの設定と一致し*ない*値に変更された場合、ミニドライバーは、WIA\_IPS\_PAGE\_size プロパティの値を、\_カスタムの WIA\_page に変更する必要があります。 また、ミニドライバーは、新しいエクステントの設定に同意するために、\_ページ\_幅または WIA\_IP\_ページの高さを\_変更する必要があります。\_

アプリケーションで WIA\_IP\_ページ\_SIZE プロパティを WIA\_PAGE\_CUSTOM に設定した場合、現在の選択領域は影響を受けません。 WIA ミニドライバーは、現在のイメージのレイアウトを取得する必要があります。これは、 [**wia\_ips\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)および[**wia\_ip\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)プロパティの現在の設定から開始します。 ページサイズの設定によって、選択領域がスキャナーのベッドの外にある場合、ミニドライバーは、WIA\_IPS\_XPOS および WIA\_IP\_YPOS プロパティの値を有効な設定に自動的に調整する必要があります。 WIA\_IP\_ページ\_SIZE と WIA\_IP\_の向きのプロパティが同時に設定され、それらが組み合わせて適用されるときに無効になる場合、ミニドライバーは[**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)メソッドでエラーを返すことによって、アプリケーションの設定を失敗させる必要があります。

ページサイズの自動検出が有効になっている場合、ドライバーは、イメージデータの転送が完了した後にのみ、正確な画像のディメンション情報を提供する必要があります。 ストリームベースの転送の場合、ドライバーは、転送の終了時にイメージヘッダー内のイメージのサイズを更新する必要があります。 新しいセッションの開始時に、WIA\_IP\_ページ\_SIZE プロパティの値は、常に、WIA\_PAGE\_AUTO 以外の値に設定する必要があります。

WIA\_PAGE\_AUTO が現在の WIA\_IP として設定されている場合\_ページ\_SIZE 値、ドライバーでは、最初に汎用イメージのサイズを含むイメージヘッダーを転送し、次にイメージデータを転送してから、転送ストリームの先頭に戻り、イメージヘッダーを実際のイメージディメンション (スキャン完了後に検出) で更新し、ストリームのインデックスをストリームの末尾に戻す必要があります。

WIA\_PAGE\_AUTO が設定されている場合 (ドライバーによって既定値として選択されているか、アプリケーションによって設定された場合)、イメージの転送全体が完了するまで、アプリケーションはイメージヘッダーに記述されているイメージのサイズを処理しないようにする必要があります。

**ただし**、wia サービス内の互換性レイヤーでは、デバイスの子項目でプロパティがサポートされていない場合に、WINDOWS XP wia デバイスから翻訳される ADF 項目に対して、WIA\_IP\_ページ\_サイズのサポートは追加されません  。 アプリケーションでは、ADF 項目が常にこのプロパティをサポートしているとは限りません。実行時に、WIA\_IP\_ページ\_サイズがサポートされているかどうかを常に確認する必要があります。 (通常、アプリケーションは、ネゴシエートされるプロパティのサポートを確認する必要があります)。

 

 

 




