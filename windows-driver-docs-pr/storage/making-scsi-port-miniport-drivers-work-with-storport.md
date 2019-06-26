---
title: SCSI ポート ミニポート ドライバーを Storport で動作させる
description: SCSI ポート ミニポート ドライバーを Storport で動作させる
ms.assetid: d2e8daaf-47e2-4a6c-9992-517dc107d4bd
keywords:
- Storport ドライバー WDK、ミニポート ドライバーの SCSI ポート
- SCSI ポート ドライバー WDK ストレージ、Storport ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63624e3036fea54a4755cfb8ecd7ff70ab47810c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386182"
---
# <a name="making-scsi-port-miniport-drivers-work-with-storport"></a>SCSI ポート ミニポート ドライバーを Storport で動作させる


## <span id="ddk_making_scsi_port_miniport_drivers_work_with_storport_kg"></span><span id="DDK_MAKING_SCSI_PORT_MINIPORT_DRIVERS_WORK_WITH_STORPORT_KG"></span>


Storport ミニポート ドライバー インターフェイスは、できるだけ、Storport ドライバーを使用する SCSI ポート ミニポート ドライバーの適合を容易にするには、SCSI ポート ミニポート ドライバー インターフェイスと同様である設計されています。 SCSI ポート ミニポート ドライバーが Storport を操作するために、次の基本的な手順を行う必要があります。

1.  すべてのインスタンスを変更、 **\#含める** &lt; *scsi.h* &gt;ディレクティブ、 **\#含める** &lt; *storport.h* &gt;ディレクティブ。

    どちらの場合、 *scsi.h*と*storport.h*ヘッダー ファイルが含まれて、コンパイル時エラーが発生します。

2.  S を置き換える*csiport.lib*で*storport.lib* 、つまり、ビルド スクリプト内では、ソースまたは**メイクファイル**ファイル。

3.  展開されたすべての構造が正しく初期化されていることを確認してください。

    両方のサイズ、 [ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)構造と[**ポート\_構成\_情報 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)構造が変更されたので、新しいメンバーが正しく初期化されています。

Storport のヘッダー ファイル、 *storport.h、* SCSI ポート プレフィックス付きのコマンドと SCSI ポートからの移植を容易に StorPort プレフィックス付きのコマンドの両方が現在保持されます。

ここでは、ドライバー作成者が SCSI のポートを使用するように設計 Storport で使えるようにミニポート ドライバーの変更を希望する詳細な手順について説明します。 次のトピックについて説明します。

[Storport をアダプターを使用するための要件](requirements-for-using-storport-with-an-adapter.md)

[Storport でハードウェアの初期化](hardware-initialization-with-storport.md)

[Storport のポート設定の構成情報](setting-port-configuration-information-with-storport.md)

 

 




