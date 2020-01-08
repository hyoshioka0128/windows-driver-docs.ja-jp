---
title: LSI_U3 デバイス用の Storport ミニポートドライバーのサンプルについて
description: LSI_U3 デバイスの Storport ミニポート ドライバーのサンプル
ms.assetid: 1ac63d07-f85c-492b-9886-f40a19d7c0b2
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 46164c2fb32b9a09d9f2288d0cf06c0550cef679
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606542"
---
# <a name="about-the-sample-storport-miniport-driver-for-an-lsi_u3-device"></a>LSI_U3 デバイス用の Storport ミニポートドライバーのサンプルについて

[LSI_U3 storport ミニポートドライバーのサンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/lsi_u3-storport-miniport-driver/
)は、scsiport ではなく storport で動作するように移植された後の、LSI の運用 SYM_U3、scsiport ベースのミニポートドライバーです。 結果として得られる Storport ベースのミニポートドライバーは、53C1010-33 または53C1010 チップを使用した LSI Ultra160 パラレル SCSI ホストバスアダプターをサポートします。 これらのホストバスアダプターの特性には、次のようなものがあります。

- インテリジェンスが最も少ない古いテクノロジ SCSI コントローラーハードウェア

- 8 KB の内部 RAM を備えた、非常にシンプルなカスタム8ビット RISC プロセッサ

- アダプターごとに256のキュータグ値を使用するように制限されたハードウェアとスクリプト

- Scsiport の機能に適合するように設計されたハードウェアとスクリプト

Storport の高度な機能をホストバスアダプター自体の限られたハードウェア機能に適合させるために、LSI_U3 ミニポートドライバーで調整が行われました。
