---
title: IStream データ転送のドライバー変更
description: IStream データ転送のドライバー変更
ms.assetid: 1c837e4f-8d53-40ed-8f5b-0d525c7dd758
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbcee2701620d01d965d8937fc1396573d57e895
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840804"
---
# <a name="istream-data-transfer-driver-changes"></a>IStream データ転送のドライバー変更


Windows Vista より前に開発されたドライバーの変更を最小限に抑えるために、ドライバーは、 **IStream**データ転送をサポートする新しいインターフェイスを実装する必要はありません。 代わりに、新しいインターフェイスが[IWiaMiniDrvCallBack インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)を介して公開されました。 ドライバーは、新しい**IWiaTransfer** callback 関数に対して**IWiaMiniDrvCallBack:: QueryInterface**を呼び出すことができます。これにより、データストリームと状態通知にアクセスできるようになります。 **IWiaTransfer**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

ファイルまたはメモリ転送の分岐ロジックを使用せずにすべての転送が同じように処理されるため、ドライバー内のデータ転送コードがより簡単になりました。

**IStream**転送モデルをサポートしていないドライバーは、通常、次の手順を実行します。

1.  フラグをチェックして、要求がアップロードまたはダウンロードのどちらであるかを確認します。

2.  [IWiaMiniDrvCallBack](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)インターフェイスを取得します。

3.  コールバック関数から変換先ストリームを受信します。

4.  データ転送ループを実行します。
    1.  デバイスからデータを受信します。
    2.  ストリームにデータを書き込みます。

ただし、新しい**IStream**転送モデルを実装するドライバーでは、*フォルダーの取得*がサポートされているため、WIA サービスは[**IWiaMiniDrv::d rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)を呼び出しません。

フォルダーの取得では、1つの転送要求が親アイテムに対して行われますが、実際のアイテムのプロパティは、転送される各子アイテムにあります。 **IWiaMiniDrv::D rvwriteitemproperties**メソッドは各子項目に対して呼び出されないため、このメソッドを使用してデバイスの設定をプログラミングすることはできません。 **IStream**データ転送をサポートするドライバーの場合、WIA サービスは[**IWiaMiniDrv::d rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)を代わりに呼び出します。

この変更は、新しいデータ転送をサポートするドライバーのみに影響する  **注意**してください。 **IStream**データ転送をサポートしていないレガシドライバーは影響を受けません。この場合、WIA サービスは**IWiaMiniDrv::D rvwriteitemproperties**メソッドの呼び出しを続けます。

 

ドライバーが**Iwiatransfercallback:: GetNextStream** (Microsoft Windows SDK のドキュメントで説明されています) に対して複数の呼び出しを行うフォルダーの取得では、ドライバーは一度に1つのアクティブなストリームしか保持できません。

ドライバーは、ダウンロード操作中に、ストリームの**istream:: Write**、 **Istream:: Seek**、および**istream:: SetSize**メソッド (Windows SDK のドキュメントで説明されています) のみを呼び出す必要があります。 この制限により、フィルターを簡単に記述できるようになります。 ドライバーでは、コピー先のストリームが他のメソッドを実装するとは限りません。

[**Wia\_DPS\_ページの\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)プロパティが\_\_wia に設定されている (ページサイズの自動検出が有効になっている) 場合、ドライバーは、イメージデータの転送が完了した後にのみ、イメージに関する正確なディメンション情報を提供する必要があります。 ストリームベースの転送の場合、ドライバーは、転送が終了したときにイメージヘッダー内のイメージのサイズを更新する必要があります。 新しいセッションの開始時に、WIA の\_DPS\_ページ\_SIZE プロパティの値は、常に、WIA\_PAGE\_AUTO 以外の値に設定する必要があります。

 

 




